Download and Installation
=========================

iVABS can be dowloaded from `its Release Page on github <https://github.com/wenbinyugroup/ivabs/releases>`_.
The folder ``Assets`` contains the installation files you need to download for different versions.
Installer contains a single executable for installation while Portable Archive contains all the files in an archive which should be extracted for installation.









Prerequisites
-------------

**VABS**

- Follow the VABS instruction to install.
- The VABS installation path ``VABS_ROOT`` should be in the environment variable ``PATH`` (and ``LD_LIBRARY_PATH`` for Linux).
- Request license from `AnalySwift <http://analyswift.com/software-trial/>`_.
  License should also be placed in the VABS installation directory.


**Python**

Version: 3.8 or above

Packages:

- numpy
- scipy
- pyyaml

For more helps on setting the Python environment, see :ref:`setup-python-env`.


Windows
-------

Below ``IVABS_ROOT`` stands for the root directory of iVABS after installation.

Installer (``ivabs-#.#-windows-installer.exe``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Select the installation folder of your own choice. The default folder is ``iVABS`` inside your home folder. You should have writing permission for the folder to install iVABS. 
#. Dakota is optional. If you would like to continue use the version of Dakota you already have on your computer, you need to uncheck the option. However, you need to make sure that Dakota binary and Dakota python library are available in the Path. 
#. Environment variables of **PATH** and **PYTHONPATH** can be updated automatically. This is needed if you want to use iVABS toolset from the command prompt.
#. A shortcut can be created in the Start Menu and Desktop.


Portable archive (``ivabs-#.#-windows-portable.7z``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Extract the archive to a folder of your own choice. 
#. Use the embeded ``env.cmd`` to automatically set up environment variables, or set up environment variables manually according to ``env.cmd``.


Setting environment variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add the following directories to ``PATH``:

- ``IVABS_ROOT/bin``
- ``IVABS_ROOT/dakota/bin`` (required only if the Dakota delivered with iVABS is used)

Add the following directories to ``PYTHONPATH``:

- ``ivabs/scripts``
- ``ivabs/dakota/share/dakota/Python`` (required only if the Dakota delivered with iVABS is used)









Linux
-----

Below ``IVABS_ROOT`` stands for the root directory of iVABS after installation.

Installer (``ivabs-#.#-linux-installer.sh``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Run

   .. code-block:: bash

      bash installer.sh

#. Select the installation folder of your own choice. The default folder is ``ivabs`` inside your home folder, i.e. ``IVABS_ROOT=~/ivabs``.
#. Dakota is optional. If you would like to continue use the Dakota already installed on your computer, you need to uncheck the option.
#. Environment variables of PATH and PYTHONPATH can be updated automatically (write to ``.bashrc`` or ``.zshrc`` file). However, if your linux box using a different shell startup file such as ``.bash_profile``, you can set these environmental variables by yourself. 


Portable archives (``ivabs-#.#-linux-portable.tar.gz``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Uncompress the archive to a folder of your own choice.

   .. code-block:: bash

      tar xzvf ivabs_#.#_linux_portable.tar.gz

#. Set environment variables manually.


Setting environment variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add the following directories to ``PATH``:

- ``IVABS_ROOT/bin``
- ``IVABS_ROOT/dakota/bin`` (required only if the Dakota delivered with iVABS is used)

Add the following directory to ``LD_LIBRARY_PATH``:

- ``IVABS_ROOT/bin``

Add the following directories to ``PYTHONPATH``:

- ``ivabs/scripts``
- ``ivabs/dakota/share/dakota/Python`` (required only if the Dakota delivered with iVABS is used)









.. _setup-python-env:

How to setup Python environment
-------------------------------

