.. Benchmarking Suite
.. Copyright 2014-2017 Engineering Ingegneria Informatica S.p.A.

.. Licensed under the Apache License, Version 2.0 (the "License");
.. you may not use this file except in compliance with the License.
.. You may obtain a copy of the License at
.. http://www.apache.org/licenses/LICENSE-2.0

.. Unless required by applicable law or agreed to in writing, software
.. distributed under the License is distributed on an "AS IS" BASIS,
.. WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
.. See the License for the specific language governing permissions and
.. limitations under the License.

.. Developed in the ARTIST EU project (www.artist-project.eu) and in the
.. CloudPerfect EU project (https://cloudperfect.eu/)

###########
Docker
###########

The Benchmarking Suite is also distributed in two different Docker containers. They are available at https://cloud.docker.com/app/benchsuite/repository/list.


benchsuite-multiexec
####################

This container can be used to run benchmarks in batch mode.

Get (or update) the image with:

.. code-block:: bash

    docker pull benchsuite/benchsuite-multiexec

Run the container binding the provider and storage (optional) configuration files stored in the local machine and passing the list of tests to execute as parameters (e.g. ``idle:idle5``):

.. code-block:: bash

    docker run -v /home/mypc/amazon.conf:/provider.conf -v /home/mypc/storage.conf:/storage.conf benchsuite/benchsuite-multiexec:dev -p provider.conf -s centos_micro idle:idle5

In case the storage service is running on the local machine, it could be necessary to use the ``--net=host`` option to reach it.

Alternatively, provider and storage configurations can be specified through environment variables: ``BENCHSUITE_PROVIDER`` and ``BENCHSUITE_STORAGE_CONFIG`` respectively.

.. code-block:: bash

    docker run -e BENCHSUITE_PROVIDER="[myconf]...." -e BENCHSUITE_SERVICE_TYPE="centos_micro" -v /home/mypc/storage.conf:/storage.conf benchsuite/benchsuite-multiexec:dev idle:idle5


.. TODO: complete section

benchsuite-rest-server
######################

This image contains the Benchmarking Suite REST SERVER (see :ref:`rest-server-doc` section). When started, the container exposes the REST service on port 5000.

To run the container, just use the Docker CLI:

.. code-block:: bash

    docker run benchsuite/benchsuite-rest-server

The service reads the Benchmarking Suite :ref:`bs-configuration` from the ``/`` directory of the container. For instance, to provide a configuration for the storage (to persist results in the db) mount a file in the container named ``/storage.conf`` or ``/storage.json``:

.. code-block:: bash

    docker run -v my-storage.conf:/storage.conf benchsuite/benchsuite-rest-server

Also providers configuration files can be mounted in the container in the same way:

.. code-block:: bash

    docker run -v my-provider.conf:/providers/my-provider.conf benchsuite/benchsuite-rest-server

