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

**********
Benchmarks
**********

The Benchmarking Suite comes with a set of third-party benchmarking tools, each of them with a set of different test configurations ready to be executed. The tools are:

- **CFD**: a tool realized in the CloudPerfect EU project [1]_ that uses OpenFOAM to run a waterbox simulation. Can be configured with different solvers, number of iterations and write to disk strategies. It is primarily a CPU intensive benchmark;
- **DaCapo**: a tool for Java benchmarking simulating real world applications with non-trivial memory loads. It is mainly a CPU and memory intensive benchmark;
- **Filebench**: a powerful and flexible tool able to generate and execute a variety of filesystem workloads to simulate applications like Web servers, File servers, Video services. It is mainly a Disk intensive benchmark;
- **Iperf**: is a tool for active measurements of the maximum achievable bandwidth on IP networks;
- **Sysbench**: a tool to test CPU, memory, file I/O, mutex performance and MySQL on Linux systems;
- **YCSB**: a tool for database benchmarking that supports several database technologies. In the Benchmarking Suite, tests for Mysql and MongoDB are provided. It is primarily a Disk intensive benchmark;
- **WebFrameworks**: tests common web frameworks workloads like fetching and inserting data in a database or create/parse json objects. It is mainly a Memory and Network intensive benchmark;


The following table summarizes the tools available and their compatibility with different operating system.

.. csv-table:: Test-OS compatibility matrix
    :widths: auto
    :header: Tool, Version, CentOS, Ubuntu 14, Ubuntu 16

    CFD,            1.0,        ✗, ✓, ✗
    DaCapo,         9.12,       ✓, ✓, ✗
    Filebench,      1.4.9.1,    ✓, ✓, ✓
    Iperf,          2.0.5,      ✗, ✓, ✓
    Sysbench,       2.1.0,      ✗, ✓, ✓
    YCSB-MySQL,     0.12.0,     ✓, ✓, ✗
    YCSB-MongoDB,   0.11.0,     ✓, ✓, ✗
    WebFrameworks,  master,     ✗, ✓, ✓


CFD
===
The CFD benchmarking tool has been realized in the context of the CloudPerfect EU project [1]_ and released open source on GitHub [2]_. The tool executes a CFD simulation on a waterbox geometry allowing to customize several parameters in order to simulate different simulations.

The following combination of parameters is used in the Benchmarking Suite tests:

.. csv-table::
    :widths: auto

    100iterGAMG, 100 iterations using the GAMG solver
    100iterWriteAtLast, 100 iterations using the GAMG solver and not writing intermediate results on the disk
    500iterGAMG, 500 iterations using the GAMG solver
    500iterGAMGWriteAtLast, 500 iterations using the GAMG solver and not writing intermediate results on the disk
    500iterICCG, 500 iterations using the ICCG solver
    500iterPCG, 500 iterations using the PCG solver

All the tests uses all the CPUs available in the machine.


Metrics
-------

.. csv-table::
    :widths: auto
    :header: Metric, Unit, Description

    duration, s, The overall duration of the simulation

DaCapo
======
DaCapo [3]_ as a tool for Java benchmarking by the programming language, memory management and computer architecture communities. It consists of a set of open source, real world applications with non-trivial memory loads. Tests implemented by the tool are:

.. csv-table:: DaCapo tests (source: http://www.dacapobench.org/)
   :widths: auto

   avrora, "simulates a number of programs run on a grid of AVR microcontrollers"
   batik, "produces a number of Scalable Vector Graphics (SVG) images based on the unit tests in Apache Batik"
   eclipse, "executes some of the (non-gui) jdt performance tests for the Eclipse IDE"
   fop, "takes an XSL-FO file, parses it and formats it, generating a PDF file."
   h2, "executes a JDBCbench-like in-memory benchmark, executing a number of transactions against a model of a banking    application, replacing the hsqldb benchmark"
   jython, "inteprets a the pybench Python benchmark"
   luindex, "Uses lucene to indexes a set of documents; the works of Shakespeare and the King James Bible"
   lusearch, "Uses lucene to do a text search of keywords over a corpus of data comprising the works of Shakespeare    and the King James Bible"
   pmd, "analyzes a set of Java classes for a range of source code problems"
   sunflow, "renders a set of images using ray tracing"
   tomcat, "runs a set of queries against a Tomcat server retrieving and verifying the resulting webpages"
   tradebeans, "runs the daytrader benchmark via a Jave Beans to a GERONIMO backend with an in memory h2 as the underlying database"
   tradesoap, "runs the daytrader benchmark via a SOAP to a GERONIMO backend with in memory h2 as the underlying database"
   xalan, "transforms XML documents into HTML"

Each test is executed multiple times, until the exectuions duration converge (variance is <= 3.0 in the latest 3 executions).

Metrics
-------

.. csv-table::
    :widths: auto
    :header: Metric, Unit, Description

    timed_duration, ms, the duration of the latest execution
    warmup_iters, num, the number of executions that were necessary to converge

Filebench
=========
Filebench [4]_ is a very powerful tool able to generate a variety of filesystem- and storage-based workloads. It implements a set of basic primitives like *createfile*, *readfile*, *mkdir*, *fsync*, ... and provide a language (the Workload Model Language - WML) to combine these primitives in complex workloads.

In the Benchmarking Suite, a set of pre-defined workloads have been used to simulate different services:

.. csv-table:: Filebench workloads (source: https://github.com/filebench/filebench/wiki/Predefined-personalities)
    :widths: auto

    fileserver, "Emulates simple file-server I/O activity. This workload performs a sequence of creates, deletes, appends, reads, writes and attribute operations on a directory tree. 50 threads are used by default. The workload generated is somewhat similar to SPECsfs."
    webproxy, "Emulates I/O activity of a simple web proxy server. A mix of create-write-close, open-read-close, and delete operations of multiple files in a directory tree and a file append to simulate proxy log. 100 threads are used by default."
    webserver, "Emulates simple web-server I/O activity. Produces a sequence of open-read-close on multiple files in a directory tree plus a log file append. 100 threads are used by default."
    videoserver, "This workloads emulates a video server. It has two filesets: one contains videos that are actively served, and the second one has videos that are available but currently inactive. One thread is writing new videos to replace no longer viewed videos in the passive set. Meanwhile $nthreads threads are serving up videos from the active video fileset."
    varmail, "Emulates I/O activity of a simple mail server that stores each e-mail in a separate file (/var/mail/ server). The workload consists of a multi-threaded set of create-append-sync, read-append-sync, read and delete operations in a single directory. 16 threads are used by default. The workload generated is somewhat similar to Postmark but multi-threaded."

Metrics
-------

.. csv-table::
    :widths: auto
    :header: Metric, Unit, Description

    duration, s, The overall duration of the test
    ops, num, The sum of all operations (of any type) executed
    ops_throughput, ops/s, The average number of operations executed per second
    throughput, MB/s, The average number of MBs written/read during the test
    cputime, µs, The average cpu time taken by each operation
    latency_avg, µs, The average duration of each operation

Iperf
=====

IPerf [5]_ is a benchmarking tool to measure the maximum achievable bandwidth on IP networks. It provides statistics both for TCP and UDP protocols.

In the Benchmarking Suite, the following pre-defined workloads have been created:

.. csv-table::
    :widths: auto

    tcp_10_1, transfer data over a single TCP connections for 10 seconds
    tcp_10_10, transfer data over 10 parallel TCP connections for 10 seconds
    udp_10_1_1, transfer UDP packets over a single connection with a maximum bandwidth limited at 1MBit/s
    udp_10_1_10, transfer UDP packets over a single connection with a maximum bandwidth limited at 10MBit/s
    udp_10_10_10, transfer UDP packets over 10 parallel connections with a maximum bandwidth limited at 1MBit/s

Metrics
-------

For the TCP workloads:

.. csv-table::
    :widths: auto
    :header: Metric, Unit, Description

    duration, s, The overall duration of the test
    transferred_x, bytes, data transferred for the connection x
    bandwidth_x, bit/s, bandwidth fo the connection x
    transferred_sum, bytes, sum of data transferred in all connections
    bandwidth_sum, bit/s, sum of bandwidth of all connections

For the UDP workloads:

.. csv-table::
    :widths: auto
    :header: Metric, Unit, Description

    duration, s, The overall duration of the test
    transferred_x, bytes, data transferred over connection x
    bandwidth_x, bit/s, bandwidth of connection x
    total_datagrams_x, num, number of UDP packets sent over connection x
    lost_datagrams_x, num, number of lost UDP packets over connection x
    jitter_x, ms, latency of connection x
    outoforder_x, num, number of packets received by the server in the wrong order
    transferred_avg, bytes, average data transferred by each connection
    bandwidth, bit/s, average bandwidth of each connection
    total_datagrams_avg, num, average number of packets sent over each connection
    lost_datagrams_avg, num, average number of packets lost for each connection
    jitter_avg, ms, average latency
    outoforder_avg, num, average number of packets received in the wrong order


Sysbench
========

SysBench [6]_ is a modular, cross-platform and multi-threaded benchmark tool for evaluating CPU, memory, file I/O, mutex performance, and even MySQL benchmarking. At the moment, in the Benchmarking Suite only the CPU benchmarking capabilities are integrated.

.. csv-table::
    :widths: auto

    cpu_10000, "Verifies prime numbers between 0 and 20000  by doing standard division of the number by all numbers between 2 and the square root of the number. This is repeated 1000 times and using 1, 2, 4, 8, 16 and 32 threads"

Metrics
-------


.. csv-table::
    :widths: auto
    :header: Metric, Unit, Description

    events_rate_X, num/s, the number of times prime numbers between 0 and 20000 are verified each second with X threads
    total_time_X, s, total number of seconds it took to execute the 1000 cycles with X threads
    latency_min_X, ms, minimum time it took for a cycle
    latency_max_X, ms, maximum time it took for a cycle
    latency_avg_X, ms, average time the 1000 cycles took. It gives a good measure of the cpu speed
    latency_95_X, ms, 95th percentile of the latency times.

YCSB
====

YCSB [7]_ is a database benchmarking tool. It has the support for several database technologies and provides a configuration mechanism to simulate different usages.

In the Benchmarking Suite, YCSB is used to benchmark two of the most popular database servers: **MySQL** and **MongoDB**.

For each database, the following workloads are executed:

.. csv-table::
    :widths: auto

    workloada, Simulates an application that performs read and update operations with a ratio of 50/50 (e.g. recent actions recording)
    workloadb, Simulates an application that performs read and update operations with a ratio of 95/5  (e.g. photo tagging)
    workloadc, Simulates a read-only databases (100% read operations)
    workloadd, Simulates an application that performs read and insert operations with a ratio of 95/5 (e.g. user status update)
    workloade, Simulates an application that performs scan and insert operations with a ratio of 95/5 (e.g. threaded conversations)
    workloadf, Simulates an application that performs read and read-modify-write operations with a ratio of 50/50 (e.g. user database)


Metrics
-------

.. csv-table::
    :widths: auto
    :header: Metric, Unit, Description

    duration, s, The overall duration of the test
    read_ops, num, THe number of read operations executed
    read_latency_avg, µs, The average latency of the read operations
    read_latency_min, µs, The minimum latency of the read operations
    read_latency_max, µs, The maximum latency of the read operations
    read_latency_95, µs, The maximum latency for the 95% of the read operations
    read_latency_99, µs, The maximum latency for the 99% of the read operations
    insert_ops, num, THe number of insert operations executed
    insert_latency_avg, µs, The average latency of the insert operations
    insert_latency_min, µs, The minimum latency of the insert operations
    insert_latency_max, µs, The maximum latency of the insert operations
    insert_latency_95, µs, The maximum latency for the 95% of the insert operations
    insert_latency_99, µs, The maximum latency for the 99% of the insert operations
    update_ops, num, THe number of update operations executed
    update_latency_avg, µs, The average latency of the update operations
    update_latency_min, µs, The minimum latency of the update operations
    update_latency_max, µs, The maximum latency of the update operations
    update_latency_95, µs, The maximum latency for the 95% of the update operations
    update_latency_99, µs, The maximum latency for the 99% of the update operations


WebFrameworks
=============
This is an open source tool [8]_ used to compare many web application frameworks executing fundamental tasks such as JSON serialization, database access, and server-side template composition. The tool has been developed and it is used to run the tests that generate the results available at: https://www.techempower.com/benchmarks/.

Currently, in the Benchmarking Suite the framework supported are: **Django**, **Spring**, **CakePHP**, **Flask**, **FastHttp** and **NodeJS**.

For each framework the following tests are executed:

.. csv-table:: Test types (source: https://www.techempower.com/benchmarks/#section=code&hw=ph)
   :widths: auto

   json, "This test exercises the framework fundamentals including keep-alive support, request routing, request header parsing, object instantiation, JSON serialization, response header generation, and request count throughput."
   query, "This test exercises the framework's object-relational mapper (ORM), random number generator, database driver, and database connection pool."
   fortunes, "This test exercises the ORM, database connectivity, dynamic-size collections, sorting, server-side templates, XSS countermeasures, and character encoding."
   db, "This test uses a testing World table. Multiple rows are fetched to more dramatically punish the database driver and connection pool. At the highest queries-per-request tested (20), this test demonstrates all frameworks' convergence toward zero requests-per-second as database activity increases."
   plaintext, "This test is an exercise of the request-routing fundamentals only, designed to demonstrate the capacity of high-performance platforms in particular. Requests will be sent using HTTP pipelining."
   update, "This test exercises the ORM's persistence of objects and the database driver's performance at running UPDATE statements or similar. The spirit of this test is to exercise a variable number of read-then-write style database operations."

For the types *json*, *query*, *fortunes* and *db* the tool executes six different burst of requests. Each burst last 15 seconds and have a different concurrency level (number of requests done concurrently): 16, 32, 64, 128, 256 and 512.

For the type *plaintext*, the tool executes four burst of 15 seconds each with the following concurrency levels: 256, 1024, 4096 and 16384.

For the type *update*, the tool executes five burst of 15 seconds each with a 512 concurrency level, but different number of queries to perform: 1, 5, 10, 15 and 20.

Metrics
-------

.. csv-table::
    :widths: auto
    :header: Metric, Unit, Description

    duration, s, The overall duration of the test
    duration_N, s, The overall duration for the N concurrency level*. It is fixed to 15 seconds by default
    totalRequests_N, num, The overall number of requests processed during the 15 seconds test at the N concurrency level*
    timeout_N, num, The number of requests that went in timeout for the N concurrency level*
    latencyAvg_N, s, the average latency between a request and its response for the N concurrency level*
    latencyMax_N, s, the maximum latency between a request and its response for the N concurrency level*
    latencyStdev_N, s, the standard deviation measure for the latency for the N concurrency level*




Adding a new benchmarking tools
===============================

In addition to the benchmarking tests coming with the standard Benchmarking Suite release, it is possible to add new benchmarking tools by providing a configuration file to instruct the Benchmarking Suite how to install, configure and execute the tool.

The configuration file must contain on section ``[DEFAULT]`` with the commands to install and execute the benchmarking tool, plus one or more sections that define different sets of input parameters to the tool. In this way, it is possible to execute the same tool to generate multiple workloads.

.. code-block:: ini

    [DEFAULT]
    class = benchsuite.stdlib.benchmark.vm_benchmark.BashCommandBenchmark


    #
    # install, install_ubuntu, install_centos_7 are all valid keys
    install_<platform> =
        echo "these are the..."
        echo "...install %(option1)s commands"

    execute_<platform> =
        echo "execute commands"

    cleanup =
        echo "commands to cleanup the %(option2)s environment"



    [workload_1]
    option1 = value1
    option2 = value

    [workload_n]
    option1 = value1
    option2 = valueN


For instance, a very minimal configuration file to integrate the Sysbench [6]_ benchmarking tool is shown below:

.. code-block:: ini

    [DEFAULT]
    class = benchsuite.stdlib.benchmark.vm_benchmark.BashCommandBenchmark

    install =
        curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.deb.sh | sudo bash
        sudo apt-get -yq install sysbench
        sysbench %(test)s prepare %(options)s

    execute =
        sysbench %(test)s run %(options)s --time=0

    cleanup =
        sysbench %(test)s cleanup %(options)s

    [cpu_workload1]
        test = cpu
        options = --cpu-max-prime=20000 --events=10000


Configuration files of the benchmarks included in the Benchmarking Suite releases can be used as starting point and are available here [10]_


.. [1] CloudPerect project homepage: http://cloudperfect.eu/
.. [2] CFD Benchmark Case code: https://github.com/benchmarking-suite/cfd-benchmark-case
.. [3] DaCapo homepage: http://www.dacapobench.org/
.. [4] Filebench homepage: https://github.com/filebench/filebench/wiki
.. [5] IPerf homepage: https://iperf.fr/
.. [6] Sysbench homepage: https://github.com/akopytov/sysbench
.. [7] YCSB homepage: https://github.com/brianfrankcooper/YCSB/wiki
.. [8] Web Framewoks Benchmarking code: https://github.com/TechEmpower/FrameworkBenchmarks
.. [10] Benchmark configuartion files: https://github.com/benchmarking-suite/benchsuite-stdlib/tree/master/data/benchmarks