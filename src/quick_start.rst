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
Quick Start
###########

Install
-------

The Benchmarking Suite is package and distributed through PyPI_.

.. important::

    The Benchmarking Suite requires Python 3.5+. If it is not the default version in you system, it is recommended
    to create a virtualenv:

        .. code-block:: bash

            virtualenv -p /usr/bin/python3.5 benchmarking-suite
            source benchsuite/bin/activate

Let's start by installing the command line tool and the standard library:

.. code-block:: bash

  $ pip install benchsuite.stdlib benchsuite.cli

This will make available the ``benchsuite`` bash command and will copy the standard benchmark tests configuration into the default configuration location (located under ``~/.config/benchmarking-suite/benchmarks``).

Configure
---------

Before executing a benchmark, we have to configure at least one Service Provider. The ``benchsuite.stdlib`` provides some template (located under ``~/.config/benchmarking-suite/providers``).

For instance, for Amazon EC2 we can start from the template and complete it:

.. code-block:: bash

    cp ~/.config/benchmarking-suite/providers/amazon.conf.example my-amazon.conf


Open and edit ``my-amazon.conf``

.. code-block:: ini

    [provider]
    class = benchsuite.provider.libcloud.LibcloudComputeProvider
    type = ec2

    access_id = <your access_id>
    secret_key = <your secret_key>

    [ubuntu_micro]
    image = ami-73f7da13
    size = t2.micro

In this case we will provide this file directly to the command line tool, but we can also configure our own configuration directory, put all our service providers and benchmarking tests configuration there and refer to them by name.

(Full specification of the configuration files syntax, can be found in the "Service Providers" sections).


Run!
----
Now you can execute your first benchmark test:

.. code-block:: bash

    benchsuite multiexec --provider my-amazon.conf --service ubuntu_micro ycsb-mongodb:workloada



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
.. _PyPI: https://python.org/pypi/benchsuite.core/
