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


####
FAQs
####


How to clear all stored benchmarking sessions?
-------------------------------------------------

Sessions are stored in a file in ``~/.local/share/benchmarking-suite/sessions.dat``. Deleting that file, all sessions will be removed. This should be an extreme solution, the more correct way to delete a session is to use the destroy-session command.

----

How to clear all stored executions?
--------------------------------------

Executions are stored along with the sessions. See previous question: `How to clear all stored benchmarking sessions?`_.