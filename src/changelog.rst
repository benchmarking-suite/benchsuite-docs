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

#########
Changelog
#########

.. consider to follow this format http://keepachangelog.com/en/1.0.0/


**********
Unreleased
**********

Added
=====
- support for MongoDB backend
- TODO list of available benchmarks and cloud providers (in Cli and REST)
- TODO field "name" in workload sections in configuration files
- TODO return node_id (in case of OpenStack) in the REST calls


**************************************
Benchmarking Suite v2.0.0 - 2017-08-01
**************************************

This is a major release  version of the Benchmarking Suite that introduces several changes and improvements with respect to the Benchmarking Suite 1.x versions.

In the Core library:

* a complete refactoring of the code to improve the parameterization and modularization
* introduction of benchmarking sessions

In the StdLib library:

* for Benchmarks:
    * NEW CFD Benchmark
    * Updated Filebench and YCSB tools versions

* for Cloud Providers:
    * NEW FIWARE FILAB connector
    * Updated Amazon EC2 to work with VPCs

The Cli and REST modules are completely new and the previous implmentation have been abandoned.
