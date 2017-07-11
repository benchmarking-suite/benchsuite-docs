###########
Quick Start
###########


The Benchmarking Suite is package and distributed through PyPI_.

.. important::

    The Benchmarking Suite requires Python 3.6+. If it is not the default version in you system, it is recommended
    to create a virtualenv:

        .. code-block:: bash

            virtualenv -p /usr/bin/python3.6 benchmarking-suite
            source benchsuite/bin/activate

Install the ``benchsuite.controller`` component:

.. code-block:: bash

  $ pip install benchsuite.stdlib benchsuite.cli



.. Before using the Benchmarking Suite, it is needed to provide a valid configuration for the benchmark tests and the
    service providers that will be managed. A good starting point is the basic configuration provided in the
    `benchmarking-configuration`_ GitHub repository. To start using it, download the repository and set the
    BENCHSUITE_CONFIG_FOLDER environment variable.


Download the basic configuration from the `benchmarking-configuration`_ GitHub repository

.. code-block:: bash

    git clone https://github.com/benchmarking-suite/benchsuite-configuration.git
    echo "export BENCHSUITE_CONFIG_FOLDER=`pwd`/benchsuite-configuration" >> ~/.bashrc
    source ~/.bashrc


.. The basic configuration contains already usable benchmarking tests, but not valid Service Provider configurations
    (because it needs user-specific information). Therefore, before using the Benchmarking Suite, you need to create your own
    Service Provider(s) configuration files.

Create your own Service Provider configuration starting from a template and filling the missing information. For
instance, to create a configuration for Amazon EC2:

.. code-block:: bash

    cp $BENCHSUITE_CONFIG_FOLDER/providers/amazon.conf.example $BENCHSUITE_CONFIG_FOLDER/providers/my-amazon.conf

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

Now you can execute your first benchmark test:

.. code-block:: bash

    python -m benchsuite.cli exec --provider my-amazon --service ubuntu_micro --tool ycsb-mongodb --workload WorkloadA

Now you can also add the rest interface

.. code-block:: bash

    pip install benchsuite.rest
    benchsuite-rest start
    tail -f benchsuite-rest.log


**********
References
**********
.. target-notes::

.. _benchmarking-configuration: https://github.com/benchmarking-suite/benchsuite-configuration
.. _PyPI: https://python.org/pypi/benchsuite.controller/