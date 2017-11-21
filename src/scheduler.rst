*********
Scheduler
*********

The Benchsuite Scheduler allows to schedule the execution of benchmarking tests at pre-fixed intervals. It needs:

* a MongoDB instance to load the **schedules** (see below), keep its state, log the executions and save the results
* a Docker Swarm instance to launch the tests (the :ref:`docker_multiexec_image` Docker image is used) and to run the scheduler itself

The scheduler works in this way:

1. loads from a MongoDB collection the :ref:`schedules` and creates a job for each schedule (it uses APScheduler_ under the hood). The jobs are kept in sync and refreshed periodically
2. sets-up a timer for each job accordingly with the time interval defined in the schedule
3. when its the time to execute a job, launchs a :ref:`docker_multiexec_image` and configure it to execute the needed tests and to store the results on another MongoDB collection


Schedules
---------

The **schedules** are the main input to the scheduler and models the tests that needs to be scheduled. Each schedule contains two types of information: the parameters of the tests and the timing information. Each schedule is expected to be a MongoDB document with this structure:

.. code-block:: json

    {
        "id" : "ec2-123asd-filebench",
        "provider_config_secret" : "ec2",
        "username" : "ggiammat",
        "tests" : [
            "filebench",
            "ycsb-mysql",
            "dacapo"
        ],
        "tags" : [
            "scheduled"
        ],
        "env" : {
            "MYVAR": "val"
        },
        "interval" : {
            "hours" : 1
        }
    }

It contains:

* ``id``: a unique id
* ``provider_config_secret``: the name (or the id) of the Docker secret that contains the Cloud Provider configuration. It uses the Docker secrets because the configuration also contains the user credentials to access the Cloud Provider
* ``username``: an identifier of the user that is requesting the execution. It will be saved also in the benchmarking results
* ``tests``: a list of test names to execute to be passed to the benchsuite ``multiexec`` command (see :ref:`cli_documentation`)
* ``tags``: a list of tags to assign to the results
* ``env``: key-value pairs that define enviornment variables to be available in the execution environment during the execution
* ``interval``: the time interval between two executions. The accepted keys are: ``weeks``, ``days``, ``hours``, ``minutes`` and ``seconds``. Multiple keys can be combined and if not specified, the default value is 0


New schedules are automatically loaded and they are rescheduled if a change is detected.


Configuration
-------------
The schduler accepts multiple parameters. Some of them are mandatory, while some other have a default value.

All the parameters can be specified in a config file in the format

.. code-block:: bash

    PARAM1=val1
    PARAM2=val2
    ...

or specified as environment variable (the latter overrides the former).

The list of mandatory parameters are:

* ``DB_HOST``: the connection string to the MongDB (e.g. "mongodb://localhost:27017"). It can be omitted only if the ``SCHEDULES_DB_HOST``, ``JOBS_DB_HOST`` and ``EXEC_DB_HOSTS`` are provided
* ``DOCKER_STORAGE_SECRET``: the name of the secret that contains the Benchsuite Storage configuration (used to store results of the tests)

The optional parameters (or the ones that have a default value) are:

* ``SCHEDULES_SYNC_INTERVAL`` (default: 60): it the number of seconds between two refresh of the schedules in the MongoDB collection
* ``SCHEDULES_JOBS_PRINT_INTERVAL`` (default: 60): interval time in seconds to print on the console a report of the scheduled and running jobs
* ``DB_NAME`` (default: "benchmarking"): the name of the MongoDB database to use
* ``SCHEDULES_DB_HOST``: if set, overrides the ``DB_HOST`` value for the MongoDB instance used to load the schedules
* ``SCHEDULES_DB_NAME``: if set, overrides the ``DB_NAME`` value for the database used to load the schedules
* ``SCHEDULES_DB_COLLECTION`` (default: "scheduling"): the name of the collection that contains the schedules
* ``JOBS_DB_HOST``: if set, overrides the ``DB_HOST`` value for the MongoDB instance used to store the internal state of the scheduler
* ``JOBS_DB_NAME``: if set, overrides the ``DB_NAME`` value for the database used to store the internal state of the scheduler
* ``JOBS_DB_COLLECTION`` (default: "_apjobs"): the name of the collection that contains the internal state of the scheduler
* ``EXEC_DB_HOST``: if set, overrides the ``DB_HOST` value for the MongoDB instance used to log the executions
* ``EXEC_DB_NAME``: if set, overrides the ``DB_NAME`` value for the database used to log the executions
* ``EXEC_DB_COLLECTION`` (default: "_apexec"): the name of the collection that contains the logs of the executions
* ``DOCKER_HOST`` (default: "localhost:2375"): the host and port of the Docker Swarm instance (used to create containers though the Docker API)
* ``DOCKER_BENCHSUITE_IMAGE`` (default: "benchsuite/benchsuite-multiexec"): the name of the benchsuite-multiexec image to use


Benchsuite Scheduler Docker image
---------------------------------

.. image:: https://img.shields.io/docker/pulls/benchsuite/benchsuite-scheduler.svg
    :target: https://hub.docker.com/r/benchsuite/benchsuite-scheduler/

The simplest way to run the Benchsuite Scheduler is to run the ``benchsuite/benchsuite-scheduler`` Docker image specifying the configuration parameters as envrionment variables:

.. code-block:: bash

   docker run -e DB_HOST=mongodb://172.17.0.1:27017/ -e DOCKER_STORAGE_SECRET=storage -e DOCKER_HOST=172.17.0.1:2375 benchsuite/benchsuite-scheduler

Alternatively, the configuration can be specified in the ``/tmp/config`` file.

.. code-block:: bash

    docker run -v /home/mypc/scheduler.conf:/tmp/config benchsuite/benchsuite-scheduler

The two approaches can be also be mixed.



.. target-notes::

.. _APScheduler: https://apscheduler.readthedocs.io/en/latest/