.. _section-ivabs-install:

Download & Installation
============

Download
-------------

iVABS can be dowloaded from `its Release Page on github <https://github.com/wenbinyugroup/ivabs/releases>`_.
The folder ``Assets`` contains the installation files you need to download for different versions.
Installer contains a single executable for installation. Portable Archive contains all the files in an archive to be extracted for installation.









Prerequisites
-------------

**VABS**

- Request VABS from `AnalySwift <http://analyswift.com/software-trial/>`_ and follow the VABS instruction to install.
- The VABS installation folder ``VABS_ROOT`` should be in the environment variable (``PATH`` for Windows and ``LD_LIBRARY_PATH`` for Linux) so that iVABS can invoke VABS executable. 
- Request license from `AnalySwift <http://analyswift.com/software-trial/>`_.
  License should also be placed inside ``VABS_ROOT``.


**Python**

Python Version: 3.8 or above is required for iVABS to run. iVABS also requires three packages: ``numpy``, ``scipy``, ``pyyaml``. For more helps on configuring the Python environment, see :ref:`setup-python-env`.







Installation
--------
..  toctree::
    :maxdepth: 1

    install/windows
    install/linux
    install/python_setup
