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



Benchsuite StdLib
=================
The Benchmarking Suite comes with a set of benchmark tests ready to be executed included in the StdLib module.
The following table summarizes the tools available and their compatibility with different operating system.

+--------------+---------+--------+-----------+
| Tool         | Version | CentOS | Ubuntu 14 |
+==============+=========+========+===========+
| CFD          | 1.0     | ✗      | ✓         |
+--------------+---------+--------+-----------+
| DaCapo       | 9.12    | ✓      | ✓         |
+--------------+---------+--------+-----------+
| Filebench    | 1.4.9.1 | ✓      | ✓         |
+--------------+---------+--------+-----------+
| YCSB-MySQL   | 0.12.0  | ✓      | ✓         |
+--------------+---------+--------+-----------+
| YCSB-MongoDB | 0.11.0  | ✓      | ✓         |
+--------------+---------+--------+-----------+


Metrics
-------
Each tool produces a set of metrics that are extracted by the Benchmarking Suite and included in the results database. The following table reports for each tool the metrics extracted and a brief description of its meaning.

+----------------+--------------------+-------+----------------------------------------------------------+
| Tool           | Metric             | Unit  | Description                                              |
+================+====================+=======+==========================================================+
| CFD            | duration           | s     | The overall duration of the test                         |
+----------------+--------------------+-------+----------------------------------------------------------+
| Filebench [1]_ | duration           | s     | The overall duration of the test                         |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | ops                |       | The sum of all the operations (of any type) executed     |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | ops_throughput     | ops/s | The average number of operations executed per second     |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | throughput         | MB/s  | The average throughput in MegaByte of the operations     |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | cputime            | µs    | The average cpu time in µs taken by each operation       |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | latency_avg        | µs    | The average latency of each operation                    |
+----------------+--------------------+-------+----------------------------------------------------------+
| YCSB  [2]_     | duration           | s     | The overall duration of the test                         |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | ops_throughput     | ops/s | The average number of operation per second executed      |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | read_ops           |       | The number of read operations executed                   |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | read_latency_avg   | µs    | The average latency for the read operations              |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | read_latency_min   | µs    | The minimum latency for the read operations              |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | read_latency_max   | µs    | The maximum latency for the read operations              |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | read_latency_95    | µs    | The maximum latency for the 95% of the read operations   |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | read_latency_99    | µs    | The maximum latency for the 99% of the read operations   |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | insert_ops         |       | The number of insert operations executed                 |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | insert_latency_avg | µs    | The average latency for the insert operations            |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | insert_latency_min | µs    | The minimum latency for the insert operations            |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | insert_latency_max | µs    | The maximum latency for the insert operations            |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | insert_latency_95  | µs    | The maximum latency for the 95% of the insert operations |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | insert_latency_99  | µs    | The maximum latency for the 99% of the insert operations |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | update_ops         |       | The number of update operations executed                 |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | update_latency_avg | µs    | The average latency for the update operations            |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | update_latency_min | µs    | The minimum latency for the update operations            |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | update_latency_max | µs    | The maximum latency for the update operations            |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | update_latency_95  | µs    | The maximum latency for the 95% of the update operations |
+----------------+--------------------+-------+----------------------------------------------------------+
|                | update_latency_99  | µs    | The maximum latency for the 99% of the update operations |
+----------------+--------------------+-------+----------------------------------------------------------+
| DaCapo         | duration           | s     | The overall duration of the test                         |
+----------------+--------------------+-------+----------------------------------------------------------+
|                |                    |       |                                                          |
+----------------+--------------------+-------+----------------------------------------------------------+

.. [1] More about the Filebench metrics can be found at https://github.com/filebench/filebench/wiki/Collected-metrics
.. [2] More about the YCSB metrics can be found at https://github.com/brianfrankcooper/YCSB/wiki/Running-a-Workload
