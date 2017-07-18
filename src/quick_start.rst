###########
Quick Start
###########

Install
-------

The Benchmarking Suite is package and distributed through PyPI_.

.. important::

    The Benchmarking Suite requires Python 3.6+. If it is not the default version in you system, it is recommended
    to create a virtualenv:

        .. code-block:: bash

            virtualenv -p /usr/bin/python3.6 benchmarking-suite
            source benchsuite/bin/activate

Let's start by installing the command line tool and the standard library:

.. code-block:: bash

  $ pip install benchsuite.stdlib benchsuite.cli

This will make available the ``benchsuite`` bash command and will copy the standard benchmark tests configuration into the default configuration location (located under ``~/.config/benchmarking-suite/benchmarks``).

Configure
---------

Before executing a benchmark, we have to configure at least one Service Provider. The ``benchsuite.stdlib`` provides some template (located under ``~/.config/benchmarking-suite/providers``).

For instance, for Amazon EC2 we can start from the template and complete it:

.. code-block::bash

    cp ~/.config/benchmarking-suite/providers/amazon.conf.example my-amazon.conf


Open and edit ``my-amazon.conf``

.. code-block:: ini

    [provider]
    class = benchsuite.provider.libcloud.LibcloudComputeProvider

    type = ec2

    access_id = <your access_id>
    secret_key = <your secret_key>

    [libcloud_extra_params]
    region = us-west-1
    ex_security_group_ids = <id of the security group>
    ex_subnet = <id of the subnet>

    [ubuntu_micro]
    image = ami-73f7da13
    size = t2.micro
    key_name = <your keypair name>
    key_path = <path to your private key file>
    vm_user = ubuntu
    platform = ubuntu_16

In this case we will provide this file directly to the command line tool, but we can also configure our own configuration directory, put all our service providers and benchmarking tests configuration there and refer to them by name (see XXX seciton).


Run!
----
Now you can execute your first benchmark test:

.. code-block:: bash

    python -m benchsuite.cli exec --provider my-amazon.conf --service ubuntu_micro --tool ycsb-mongodb --workload WorkloadA



Go REST
--------

Enable the REST server is very simple:

.. code-block:: bash

    pip install benchsuite.rest
    benchsuite-rest start
    tail -f benchsuite-rest.log

References
----------

.. target-notes::

.. _benchmarking-configuration: https://github.com/benchmarking-suite/benchsuite-configuration
.. _PyPI: https://python.org/pypi/benchsuite.controller/
