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

The Benchmarking Suite comes with a set of benchmark tests ready to be executed included in the StdLib module.
The following table summarizes the tools available and their compatibility with different operating system.

.. csv-table:: Test-OS compatibility matrix
    :widths: auto
    :header: Tool, Version, CentOS, Ubuntu 14, Ubuntu 16

    CFD, 1.0, ✗, ✓,
    DaCapo, 9.12, ✓, ✓,
    Filebench, 1.4.9.1, ✓, ✓,
    YCSB-MySQL, 0.12.0, ✓, ✓,
    YCSB-MongoDB, 0.11.0, ✓, ✓,
    WebFrameworks, master, , , ✓


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

YCSB
====

YCSB [5]_ is a database benchmarking tool. It has the support for several database technologies and provides a configuration mechanism to simulate different usages.

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
This is an open source tool [6]_ used to compare many web application frameworks executing fundamental tasks such as JSON serialization, database access, and server-side template composition. The tool has been developed and it is used to run the tests that generate the results available at: https://www.techempower.com/benchmarks/.

Currently, in the Benchmarking Suite the framework supported are: **Django**, **Spring** and **CakePHP**.

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

.. [1] CloudPerect project homepage: http://cloudperfect.eu/
.. [2] CFD Benchmark Case code: https://github.com/benchmarking-suite/cfd-benchmark-case
.. [3] DaCapo homepage: http://www.dacapobench.org/
.. [4] Filebench homepage: https://github.com/filebench/filebench/wiki
.. [5] YCSB homepage: https://github.com/brianfrankcooper/YCSB/wiki
.. [6] Web Framewoks Benchmarking code: https://github.com/TechEmpower/FrameworkBenchmarks
