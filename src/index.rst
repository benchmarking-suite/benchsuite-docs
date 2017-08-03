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

##############################################
Welcome to Benchmarking Suite's documentation!
##############################################



The Benchmarking Suite is an all-in-one solution for benchmarking cloud services simulating different typical application behaviours and comparing the results on different cloud providers. It wraps a set of representative, de-facto standard and widely used third-party benchmarking tools and relies on them for the workload simulation and performance measurement.

The Benchmarking Suite automates the benchmarking process managing the allocation and de-allocation of necessary resources, the installation and execution of the benchmarking tools and the storage of data.

It has been designed to be extendible and allow an easy integration of new third-party benchmarking tools and cloud services. Data collected and stored during the tests execution is homogenized and aggregated on different higher-level metrics (e.g. average value) allowing performance comparisons among different providers and/or different dates.

The Benchmarking Suite development has been funded by two European reasearch and innovation projects: ARTIST_ and CloudPerfect_. 


License
=======
The Benchmarking Suite is an open source product released under the `Apache License v2.0`_.


Topics
==========

.. toctree::
   :maxdepth: 2

   quick_start
   architecture
   configuration
   executions
   cli
   rest
   docker
   API
   changelog
   development
   faq


Contacts
========

Main contact person for the Benchmarking Suite is:

:Person:
    Gabriele Giammatteo

:Company:
    Research and Development Laboratory
    Engineering Ingegneria Informatica S.p.A.
    
:Address:
    via Riccardo Morandi, 32
    00148 Rome, Italy

:e-mail:
    gabriele.giammatteo@eng.it

For bugs, features and other code-related requests the issue tracker can be used at:
https://github.com/benchmarking-suite/benchsuite-core/issues


References
==========

.. target-notes::

.. _ARTIST: http://www.artist-project.eu/
.. _CloudPerfect: https://cloudperfect.eu/
.. _`Apache License v2.0`: https://www.apache.org/licenses/LICENSE-2.0    
