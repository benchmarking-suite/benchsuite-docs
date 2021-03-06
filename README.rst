Benchmarking Suite documentation
================================

Documentation
=============
User and technical documentation is available at http://benchmarking-suite.readthedocs.io/.

Support
=======

For bugs, enhancements or support go to https://github.com/benchmarking-suite/benchsuite-issues/issues/.

Build
=====

To build the documentation locally:

.. code-block:: bash

    $ pip install -r requirements.txt
    $ pip install sphinx_rtd_theme
    $ sphinx-build -b html src/ build/

To start a development server that rebuilds documentation automatically on change:

.. code-block:: bash

    $ pip install sphinx-autobuild
    $ sphinx-autobuild src/ build/

Legal
=====
The Benchmarking Suite is released under the `Apache 2.0 <https://www.apache.org/licenses/LICENSE-2.0>`_ license.

Copyright © 2014-2018 Engineering Ingegneria Informatica S.p.A. All rights reserved.

+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
| .. image:: http://www.consilium.europa.eu/images/img_flag-eu.gif |This work has received partial funding from the European Commission under grant agreements No. FP7-317859 and No. H2020-732258|
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
