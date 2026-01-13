################################
Generate and view documentation
################################

When everything is installed, in this very folder, you can generate the documentation with the following command:

.. code-block:: bash
   
   source .venv/bin/activate
   make html
   firefox build/html/index.html

***********************************
Install the documentation locally
***********************************

To install the documentation locally, you can use the following command:

.. code-block:: bash

   sudo apt-get update
   sudo apt-get install -f python3-venv python3-sphinx
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
