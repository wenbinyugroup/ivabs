.. _section-ivabs-start:

Quick Start
============

..  note::

    In the instructions below ``$IVABS_ROOT`` refers to the root directory of iVABS after installation.




Run iVABS with a simple example
-------------------------------

Start the shell/terminal that is configured for the installation.

Optionally change the python virtual environment.
For example, if Python 3 and all dependencies are installed in a virtual environment named ``py3ivabs`` using Anaconda, then activate it using

..  code-block:: shell

    conda activate py3ivabs

Go to the directory ``$IVABS_ROOT/examples/e0_quickstart``

..  code-block:: shell

    cd $IVABS_ROOT/examples/e0_quickstart

Run the example

..  code-block:: shell

    python run.py cs_param_study.yml

If everything works fine, several output files will be generated.
In the file ``cs_param_study.out``, the following message should appear.

..  code-block:: none

    <<<<< Iterator multidim_parameter_study completed.
    <<<<< Environment execution completed.
    DAKOTA execution time in seconds:
    Total CPU        =     34.003 [parent =     34.003, child =          0]
    Total wall clock =     34.003

This example runs about half minute.




Files of this example
---------------------





iVABS running options
---------------------


Other examples
--------------

More examples can be found in Section :ref:`section-ivabs-examples`.
