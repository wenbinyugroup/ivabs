.. _section-ivabs-start:

Quick Start
============

..  note::

    ``IVABS_ROOT`` refers to the root directory of iVABS after installation.




Run iVABS with a simple example
-------------------------------

Start the shell/terminal that is configured during the installation.
Please refer to :ref:`section-ivabs_install` for more information.

    If you are using Python virtual environment managed by Anaconda (see :doc:`/ivabs/install/python_setup`), you need to activate it first.
    For example, if Python 3.6 and all dependencies are installed in a virtual environment named ``py3ivabs``, then activate it using

    ..  code-block:: shell

        conda activate py3ivabs

Go to the directory ``IVABS_ROOT/examples/e0_quickstart``

..  code-block:: shell

    cd IVABS_ROOT/examples/e0_quickstart

Run the example using the following command.
Note: The actual Python command may vary depending on your environment setup, such as ``python`` or ``python3``.

..  code-block:: shell

    python run.py cs_param_study.yml

If iVABS has been installed properly, it will generate a complete list of output files shown in the section below (:ref:`section-start_file_out`).
In the file ``cs_param_study.out``, the following message should appear at the end of the file.

..  code-block:: none

    <<<<< Iterator multidim_parameter_study completed.
    <<<<< Environment execution completed.
    DAKOTA execution time in seconds:
    Total CPU        =     34.003 [parent =     34.003, child =          0]
    Total wall clock =     34.003

Running time usually takes less than one minute depending on the computer.

Please refer to :ref:`section-ivabs_example_quickstart_param_study` for a detailed explanation of this example. 



iVABS running options
---------------------

The general command syntax to run an iVABS study is

..  code-block:: shell

    python run.py main_input.yml [mode] [dakota_params.in dakota_results.out]

There are three running modes:

#. Mode 0 is the default mode. It will generate Dakota input and run.

   ..  code-block:: shell

    python run.py main_input.yml


#. Mode 1 runs a single analysis. This mode is designed to use the simple iVABS interface to run PreVABS without using Dakota. 

#. Mode 2 only generates Dakota input. The process stops after generating the Dakota input.

   ..  code-block:: shell

    python run.py main_input.yml 2






Other examples
--------------

More examples can be found in Section :ref:`section-ivabs-examples`.
