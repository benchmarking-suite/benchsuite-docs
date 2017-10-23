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


**************************************
Benchmarking Suite v2.2.2
**************************************
Release date: 2017-10-20

This patch release fixes some minor bugs found in the code:

- fixed creation of new sessions if the provider configuration is in json format
- fixed default error handling in the REST server (now the full exception message - and not only "Internal Server Error" is sent back to the caller)
- fixed parsing of "network" and "security_group" parameters: now they can be either the id or the name of the object
- fixed crash of some Filebench workloads on Amazon EC2 using the micro instances


**************************************
Benchmarking Suite v2.2.1
**************************************
Release date: 2017-10-18


This patch release fixes an outdated information in the REST server documentation page


**************************************
Benchmarking Suite v2.2.0
**************************************
Release date: 2017-10-18

This minor release introduces following improvements:

- support for json configuration files (only for providers and storage at the moment)
- better handling of network configuration parameters in the provider configuration


**************************************
Benchmarking Suite v2.1.0
**************************************
Release date: 2017-10-13

This minor release introduces some new functionalities and improvement to the tool:

- support for MongoDB backend
- list of available benchmarks and cloud providers (in Cli and REST)
- field "name" in workload sections in configuration files
- return node_id (in case of OpenStack) in the REST calls
- accept provider configuration as string parameter
- add tags to sessions/executions (e.g. for the user-id in the QET)
- provider and storage configurations can be also specified via command line or environment variable
- improvement and tuning of YCSB, Filebench and DaCapo benchmarks


**************************************
Benchmarking Suite v2.0.0
**************************************
Release date: 2017-08-01

This is a major release version of the Benchmarking Suite that introduces several changes and improvements with respect to the Benchmarking Suite 1.x versions.

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
