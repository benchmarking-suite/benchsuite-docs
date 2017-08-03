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
Development
###########


Continuous Integration
======================

TBD


Release Steps
=============

Checklist to release the Benchmarking Suite

For each module to release:

1. increase the version number in the ``__init__py`` file
   
2. create the source distribution package and upload on PYPI (remove the ``-r pypitest`` to upload on the official PYPI)

   .. code-block:: bash

    python setup.py sdist upload -r pypitest
   
3. commit and push everything on GitHub

4. create a tag on GitHub

