.. _section-ivabs_python:

Setup Python Environment
==================================

..  note::

    The following instruction is mainly based on the developers' machine (Windows 10 and CentOS Linux 7).
    Some steps and commands could be different for your machine, especially for Linux.
    If your machine is maintained by your IT department, you can ask them for help.


There are many ways to setup a Python environment.
As long as the prerequisites for Python (:ref:`section-ivabs_prerequisites`) are met, you can do this in your own way.







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

Follow the official instructions for installation: https://conda.io/projects/conda/en/latest/user-guide/install/index.html.


Windows
^^^^^^^^


Linux
^^^^^^^

Depending on the system configuration and package management, you may need to load the anaconda module before using it the first time::

  module load anaconda

.. After installation and configuration, the command prompt should look like the following (could be slightly different depending on the shell/terminal):

.. ..  code-block:: shell

..     (base) user_name@machine_name: ~$

.. where ``base`` is the name of the globally default virtual environment.

**Manage virtual environment**

To create a virtual environment named ``py3ivabs`` with Python 3.6 and required packages, run

..  code-block:: shell

    conda create --name py3ivabs python=3.6 numpy scipy pyyaml

To switch to the new virtual environment, run

..  code-block:: shell

    conda activate py3ivabs

If this is your first time activating this environment, you may some error message printed.
Follow the instruction in that message to configure your shell.
More instructions can be found in the official documentation: https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#activating-an-environment.

Then the command prompt should be something like:

..  code-block:: shell

    (py3ivabs) user_name@machine_name: ~$






For more detailed instructions, see `official documentation <https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`_


