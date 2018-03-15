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


.. _rest-server-doc:

##############
REST Server
##############


Quick Start
###########

This short tutorial shows how to use the API to perform a step-by-step benchmarking test.

First, we need to create a new session. This can be done making a ``POST`` request to ``/api/v1/sessions`` providing the provider name and service type.

.. code-block:: bash

    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{\
        "provider": "my-provider",\
        "service": "my-service-type"\
    }' http://localhost:5000/api/v1/sessions

Alternatively, the provider configuration can be provided directly in the request payload. For instance, a typical request to create a benchmarking session for Amazon EC2 would be:

.. code-block:: bash

    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{\
        "config": {\
            "provider": {\
                    "class": "benchsuite.stdlib.provider.libcloud.LibcloudComputeProvider",\
                        "name": "ec2-ggiammat",\
                        "driver": "ec2",\
                        "access_id": "<your_access_id>",\
                        "secret_key": "<your_key>",\
                        "region": "us-west-1"\
                },\
                "centos_micro": {\
                        "image": "ami-327f5352",\
                        "size": "t2.micro",\
                        "vm_user": "ec2-user",\
                        "platform": "centos_6",\
                        "key_name": "<keypair_name>",\
                        "ssh_private_key": "----BEGIN RSA PRIVATE KEY-----\nIIE... [...] ...6alL\n-----END RSA PRIVATE KEY-----"\
                }\
        }\
    }' http://localhost:5000/api/v1/sessions/


.. important::

    Providing the configuration directly in the request payload, your credentials will be sent over the network unencrypted. Do it only when the server is running in a trusted environment!

.. note::

    The ssh private key msut be provided on a sinlge line (json does not support multiline values), but the line ends must be preserved. A convenient method to generate this string in bash is:

    .. code-block:: bash

        sed -E ':a;N;$!ba;s/\r{0,1}\n/\\n/g' my-key.pem


The response will contain the ``id`` of the session created:

.. code-block:: json

    {
        "id": "58920c6c-c57c-4c55-a227-0ab1919e83be",
        [...]
    }

Now we can create a new benchmarking test execution in the session (note that the id of the session is used in the request URL:

.. code-block:: bash

    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
        "tool": "idle", \
        "workload": "idle30" \
    }' http://localhost:5000/api/v1/sessions/58920c6c-c57c-4c55-a227-0ab1919e83be/executions/


The response will contain (along with other execution details) the ``id`` of the execution:

.. code-block:: json

    {
        "id": "253d9544-b3db-11e7-8bc2-742b62857160",
        [...]
    }

With this execution id we can now invoke the *prepare* step that will create the resources on the provider, install the necessary tools and load the workloads:

.. code-block:: bash

    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:5000/api/v1/executions/253d9544-b3db-11e7-8bc2-742b62857160/prepare

Finally, we can invoke the *run* step:

.. code-block:: bash

    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:5000/api/v1/executions/253d9544-b3db-11e7-8bc2-742b62857160/run

The response of the *prepare* and *run* steps contain the start time and the duration of the operation:

.. code-block:: bash

    {
        "started": "2017-10-18 08:18:33",
        "duration": "32.28253793716431"
    }


The same session can be used to run multiple executions. At the end, the session and the resources created (e.g. VM) can be destroyed using the DELETE operation:

.. code-block:: bash

    curl -X DELETE --header 'Accept: application/json' http://localhost:5000/api/v1/sessions/58920c6c-c57c-4c55-a227-0ab1919e83be

Swagger Doc
###########

This documentation is autogenerated from the Swagger API Specification using `sphinx-swaggerdoc`_.

A better documentation for the REST API can be found directly in the REST Server:

1. Launch the server
2. Open http://localhost:5000/api/v1/


.. swaggerv2doc:: file://{{currentDir}}/swagger-api.json


..  _sphinx-swaggerdoc: https://github.com/unaguil/sphinx-swaggerdoc