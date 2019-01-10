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

*****************
Service Providers
*****************

Configuration
-------------
Each provider has its own configuration file that provides all the information to access and use the provider plus the configuration of the services offered by the provider (e.g. VM creation). The configuration is specified in a properties file (also in JSON format). The list of supported properties is shown below (see on GitHub_):

.. code-block:: ini

    #
    # PROVIDER SECTION
    #
    #

    [provider]

    #
    # MANDATORY FIELDS
    #

    # the Benchmarking Suite class that implement the access to this provider
    class = benchsuite.stdlib.provider.libcloud.LibcloudComputeProvider

    # custom human-readable name for the provider. Used only for displaying purposes
    name = ote-testbed

    # the driver that Libcloud should use to access the provider
    driver = openstack

    # Access credentials
    access_id = admin
    secret_key = xxxxx

    # Authentication URL for the target Cloud
    auth_url = http://cloudpcntlr:5000/


    #
    # OPTIONAL FIELDS
    #

    # If not specified RegionOne is used
    region = RegionOne

    # if not specified 2.0_password and 3.x_password will be attempted
    auth_version = 3.x_password

    # if not specified, a new security group "benchsuite_sg" will be created (if
    # not exist)
    security_group = mysg

    # Automatically selected if multiple exist
    network = mynet

    # If not specified the access_id is used
    tenant = admin

    # If specified do not attemp to assign a public IP
    benchsuite.openstack.no_floating_ip = true


    # after a new VM is created, a connection test is executed to check that everything
    # is ok and to execute the post-creation scripts.
    new_vm.connection_retry_period = 30
    new_vm.connection_retry_times = 10


    #
    # SERIVCE TYPE SECTIONS
    #
    #

    [ubuntu_large]

    #
    # MANDATORY FIELDS
    #

    image = base_ubuntu_14.04
    size = m1.large


    #
    # OPTIONAL FIELDS
    #

    # name of the keypair to assign to the VM. If not specified, a new keypair will
    # be created and then removed after the test ends.
    key_name = ggiammat-key

    # file that contains the private key. Alternatively the private key can be
    # specified in this config file directly with the ssh_private_key property
    key_path = /home/ggiammat/credentials/filab-vicenza/ggiammat-key.pem

    # optional way to specify the key directly in the configuration instead
    # of by filename
    ssh_private_key = -----BEGIN RSA PRIVATE KEY-----
        MIIEowIBAAKCAQEAkadPr5n1NSOyHloajvovCD05M5Gz36NN4UouSWmId8QuTwXx
        Hw6m9aOXJmYHdkSYLrNs+y65EDpUkw1DXNDEJ146ZK9PxAQEdcngwPk76a4A/ybz
        [...]
        x+GRpQ9o/4EAzpBw9NVNNJ9Glbd7SSFqhpHR5pn5OBG/fdPJV8DzjUET528o8Jd9
        gynGwAYRed38UtCE7gn+u1RSvmYUveDwQ7Cf2KIohI2jlzR6YLea
        -----END RSA PRIVATE KEY-----

    # If not specified, the Benchmarking Suite will try to guess them
    vm_user = ubuntu
    platform = ubuntu

    # any command to run just after the VM has been created
    post_create_script =
        sudo hostname localhost


.. target-notes::

.. _GitHub: https://github.com/benchmarking-suite/benchsuite-stdlib/blob/master/data/providers/openstack.conf.example
