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

This section explains the development, integration and distritbuion process of the Benchmarking Suite. Intended readers are developers.

Continuous Integration
======================

TBD


Release Steps
=============

Checklist to release the Benchmarking Suite


1. Commit any not-committed file on the workspace

2. Identify whcih modules needs to be released (see commits since the latest release, see the changelog)

3. Update the changelog file if not done (use messages in the commits as reference)


Modules Release
---------------

For each module to release:

1. increase the version number in the ``__init__py`` file
   
2. create the source distribution package and upload on PYPI Testing (remove the ``-r pypitest`` to upload on the official PYPI)

   .. code-block:: bash

    python setup.py sdist upload -r pypitest

3. to test the release from PYPI test:

   .. code-block:: bash

    # create a new virtual env
    virtualenv -p /usr/bin/python3.5 venvXX

    # activate the virtualenv
    source venvXX/bin/activate


    # install the modules to test
    pip install -v -i https://testpypi.python.org/pypi --extra-index-url https://pypi.python.org/simple/ -U benchsuite.core


4. upload the distribution packages on PYPI

    .. code-block:: bash

        python setup.py sdist upload

3. commit and push everything on GitHub

4. create a release on GitHub (this will also create a tag)


Milestone Release
-----------------

1. Check all the modules and the versions that will be included. Release modules if necessary

1. In ``benchsuite-docs``, update the version in conf.py

2. Update the changelog.rst with the changelog for this milestone

6. Commit the documentation on GitHub and create a tag. This will also create a new tag in readthedocs

7. Update the ".release" Dockerfiles in benchsuite-docker project

8. Commit benchsuite-docker and create a new tag. This will trigger the creation of a new tag for docker images


Documentation
=============

Documentation is automatically built on ReadTheDocs at every commit


Docker
======

Docker containers are built automatically from Dockerfiles located in the benchsuite-docker repository.

To create a new tag of Docker images, create a tag in the Git repository that starts with "v" (e.g. "v2.0", "v1.2.3", "v1.2.3-beta1", ...)