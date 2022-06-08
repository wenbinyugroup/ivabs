.. _section-ivabs_python:

Setup Python Environment
==================================

It is highly recommended to create a local virtual Python environment and run iVABS in it.
The benefit is that the virtual environment is completely in the control of the local user and won't affect and be affected by the global environment.

The recommended way to setup a virtual environment is through Anaconda.


..  contents:: Contents
    :depth: 3
    :local:
    :backlinks: none



Anaconda
---------



Installation
~~~~~~~~~~~~~

Windows
^^^^^^^^


Linux
^^^^^^^

Load the anaconda module.

After installation and configuration, the command prompt should look like the following (could be slightly different depending on the shell/terminal):

..  code-block:: shell

    (base) user_name@machine_name: ~$

where ``base`` is the name of the globally default virtual environment.

Manage virtual environment
~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a virtual environment named ``py3ivabs`` with Python 3.6 and required packages, run

..  code-block:: shell

    conda create --name py3ivabs python=3.6 numpy scipy pyyaml

To switch to the new virtual environment, run

..  code-block:: shell

    conda activate py3ivabs

Then the command prompt should be something like:

..  code-block:: shell

    (py3ivabs) user_name@machine_name: ~$


For more detailed instructions, see `official documentation <https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`_

