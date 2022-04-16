Download and Installation
=========================

iVABS can be dowloaded from `its Release Page on github <https://github.com/wenbinyugroup/ivabs/releases>`_ (click  `here <https://github.com/wenbinyugroup/ivabs/releases>`_ ).
The folder ``Assets`` contains the installation files you need to download for different versions.
Installer contains a single executable for installation while Portable Archive contains all the files in an archive which should be extracted for installation.


Prerequisites
-------------

VABS
~~~~

- Follow the VABS instruction to install.
- The VABS installation path ``VABS_ROOT`` should be in the environment variable ``PATH`` (and ``LD_LIBRARY_PATH`` for Linux).
- Request license from `AnalySwift <http://analyswift.com/software-trial/>`_.
  License should also be placed in the VABS installation directory.

Python
~~~~~~

Version: 3.8 or above

Packages:

- numpy
- scipy
- pyyaml



Windows
-------

Installer (files with extension ``exe``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Select the installation folder of your own choice. The default folder is ``iVABS`` inside your home folder. You should have writing permission for the folder to install iVABS. 
#. Dakota is optional. If you would like to continue use the version of Dakota you already have on your computer, you need to uncheck the option. However, you need to make sure that Dakota binary and Dakota python library are available in the Path. 
#. Environment variables of **PATH** and **PYTHONPATH** can be updated automatically. This is needed if you want to use iVABS toolset from the command prompt.
#. A shortcut can be created in the Start Menu and Desktop.


Portable archive (files with extension ``7z``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Extract the archive to a folder of your own choice. 
#. Use the embeded ``env.cmd`` to automatically set up environment variables, or set up environment variables manually according to ``env.cmd``.


Setting environment variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~




Linux
-----

Installer (files with extension ``sh``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Excute the installer ``bash installer.sh``.
#. Select the installation folder of your own choice. The default folder is ``iVABS`` inside your home folder.
#. Dakota is optional. If you would like to continue use the version of Dakota you already have on your computer, you need to uncheck the option. However, you need to make sure that Dakota binary and Dakota python library are available in the Path. 
#. Environment variables of PATH and PYTHONPATH can be updated automatically (write to ``.bashrc`` or ``.zshrc`` file). However, if your linux box using a different file such as .bash_profile for storing these variables, you can set these environmental variables by yourself. 


Portable archives (files with extension ``tar.gz``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Uncompress the archive using ``tar xzvf ivabs_x.x_linux64_portable.tar.gz`` to a folder of your own choice. 
#. Set environment variables manually.


Setting environment variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- ``ivabs\bin`` should be in **PATH**. 
- ``ivabs\vendors\dakota\share\dakota\Python`` should be in **PYTHONPATH**. Use the corresponding Dakota Python PATH if you want to use the Dakota already installed on your computer.
- ``ivabs\vendors\msgpi`` should be in **PYTHONPATH**.

