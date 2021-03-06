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

This Changelog reports the main changes occuring in the Benchmarking Suite. The versions of the Benchmarking Suite (also called Milestones) refers to the versions of the Docker containers and the Documentation, while the versions of the single modules are reported in each entry of the changelog.

The Unreleased_ section contains changes already released in the Python modules, but not yet included in any Milestone.

**********
Unreleased
**********

**************************************
Benchmarking Suite v. 3.1.0
**************************************
Release date: 2019-01-17

- [stdlib-2.7.0] reduced number of testing queries for YCSB benchmarks (reducing the overall duration of the tests)
- [stdlib-2.7.0] added Ubuntu 14 compatibility for Web Framework benchmark
- [stdlib-2.7.0] more robust ssh connections (retry on network failure for a fixed number of times)
- [stdlib-2.7.0] new version of Paramiko ssh library that brings security patches
- [stdlib-2.7.0] increasing waiting time in YCSB test for MongoDB to start
- [stdlib-2.7.0] implemented multi-node benchmark tests with custom number and names of nodes
- [stdlib-2.7.0] added IPerf benchmark with various pre-defined workloads
- [stdlib-2.7.0] added Sysbench benchmark with various pre-defined workloads
- [core-2.6.0] added option to keep the environment after a multiexec execution
- [core-2.6.0] added option in multiexec mode to retry a failed test
- [core-2.6.0] added option to retry (--max-retry) tests if they fail
- [core-2.6.0] improved handling of logs in multi-node tests
- [core-2.6.0] improved execution of clean-up scripts
- [scheduler-1.5.0] improved logging of executions
- [scheduler-1.5.0] added debug option that not delete containers after they end
- [backends-2.5.0] updated result records schema to version 2: include all logs of multi-node tests
- [cli-2.3.0] improved log messages


**************************************
Benchmarking Suite v. 3.0.0
**************************************
Release date: 2018-08-08

- [stdlib-2.6.0] added Web Frameworks Benchmarking tool
- [stdlib-2.6.0] added category and keywords for each workload
- [stdlib-2.6.0] auto-discovery (when possible) of networks, security groups and platforms
- [stdlib-2.6.0] add async executions to avoid timeout exceptions
- [stdlib-2.6.0] support creation of key pairs if not provided in the configuration
- [scheduler-1.4.0] updated to docker-py version 3.0.0
- [scheduler-1.4.0] improved logging of exceptions
- [scheduler-1.4.0] added "properties" field in schedules to store custom data in generated results
- [cli-2.2.0] introduced autocomplete for some commands
- [backends-2.4.0] store execution errors and logs in the backend
- [backends-2.4.0] changed results schema
- [core-2.5.0] fixed crash if the storage was not properly configured
- [core-2.5.0] allowed to use wildecards in workload names in multiexec mode


**************************************
Benchmarking Suite v. 2.7.0
**************************************
Release date: 2018-02-14

- [rest-2.3.0] added options to listen on specific host and port
- [sdtlib-2.5.0] customizable retries time for connection to new VMs
- [stdlib-2.5.0] delete the VMs created in case of an unhandled exception during the creation
- [stdlib-2.5.0] fixed empty values in configuration parsing
- [core-2.4.0] added possibility to use custom sessions storage file
- [scheduler-1.3.1] fixed invalid characters in containers name

**************************************
Benchmarking Suite v. 2.6.1
**************************************
Release date: 2018-01-22

- [stdlib-2.4.3] support for 'auth_url', 'auth_version' and 'region' provider config parameters

**************************************
Benchmarking Suite v. 2.6.0
**************************************
Release date: 2018-01-16

- [scheduler-1.3.0] added configuration parameters to add additional Docker options to the containers created by the scheduler

**************************************
Benchmarking Suite v. 2.5.1
**************************************
Release date: 2018-01-15

- fixed the URL to download the DaCapo benchmark


**************************************
Benchmarking Suite v. 2.5.0
**************************************
Release date: 2017-12-18

- [backends-2.3.0] MongoDB - storing start time as date object (previously it was a timestamp)
- [scheduler-1.2.0] Support for using Docker unix socket instead of the tcp port
- [core-2.3.1] Fixed DEFAULT section not read in the Json configuration files
- [stdlib-2.4.1] Fixed serialization issue of the LibcloudComputeProvider objects
- [cli-2.1.2] Improvements and fixes to the "shell" command


**************************************
Benchmarking Suite v. 2.4.0
**************************************
Release date: 2017-12-04

- [stdlib-2.4.0] randomize names of VMs created by the Benchmarking Suite
- [stdlib-2.4.0] set security groups in openstack
- [scheduler-1.1.0] add config parameter to add global env, tags and additional params
- [scheduler-1.1.0] added the "active" parameter in the schedules
- [core-2.3.0, backends-2.2.0] added storage of execution errors in the database


**************************************
Benchmarking Suite v. 2.3.1
**************************************
Release date: 2017-11-21

- [core-2.2.4] fixed support for the --failonerror parameter from the command line

**************************************
Benchmarking Suite v. 2.3.0
**************************************
Release date: 2017-11-20

- [core-2.2.2] considering only providers configuration files with extension .json and .conf
- [core-2.2.3] duration is now considered as a metric
- [stdlib-2.3.0] metrics renamed to make them coherent in different tests
- [stdlib-2.3.0] added multiple workloads in the CFD benchmark
- [cli-2.1.1] added --failonerror for the multiexec command. The option allows to not continue with next test if the current one fails
- [scheduler-1.0.0] first release of the Benchsuite Scheduler


**************************************
Benchmarking Suite v. 2.2.2
**************************************
Release date: 2017-10-20

This patch release fixes some minor bugs found in the code:

- fixed creation of new sessions if the provider configuration is in json format
- fixed default error handling in the REST server (now the full exception message - and not only "Internal Server Error" is sent back to the caller)
- fixed parsing of "network" and "security_group" parameters: now they can be either the id or the name of the object
- fixed crash of some Filebench workloads on Amazon EC2 using the micro instances


**************************************
Benchmarking Suite v. 2.2.1
**************************************
Release date: 2017-10-18


This patch release fixes an outdated information in the REST server documentation page


**************************************
Benchmarking Suite v. 2.2.0
**************************************
Release date: 2017-10-18

This minor release introduces following improvements:

- support for json configuration files (only for providers and storage at the moment)
- better handling of network configuration parameters in the provider configuration


**************************************
Benchmarking Suite v. 2.1.0
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
Benchmarking Suite v. 2.0.0
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
