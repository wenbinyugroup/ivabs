.. _section-ivabs_install:

Download & Installation
========================

Download
-------------

iVABS can be dowloaded from `its Release Page on github <https://github.com/wenbinyugroup/ivabs/releases>`_.
The directory ``Assets`` contains the installation files you need to download for different versions.
Please ignore ``Source code (zip)`` and ``Source code (tar.gz)`` because they just contain files used to generate this documentation site.
Package with ``installer`` in the file name contains a single executable for the automatic installation.
Package with ``portable`` in the file name contains all the files in an archive requiring manual extraction and setting up. Packages are released for both Windows and Linux. 



Prerequisites
-------------

**VABS**

- Request VABS from `AnalySwift <http://analyswift.com/software-trial/>`_ and follow the VABS instruction to install.
- The VABS installation directory ``VABS_ROOT`` should be in the environment variable (``PATH`` for Windows/Linux and ``LD_LIBRARY_PATH`` for Linux) so that iVABS can invoke the VABS executable. 
- Request license from `AnalySwift <http://analyswift.com/software-trial/>`_.
  License should also be placed inside ``VABS_ROOT``.


**Python**

Python 3.6 or above is required for iVABS to run. Packages ``numpy``, ``scipy``, and ``pyyaml`` should also be properly installed. 
For help on configuring the Python environment, see :doc:`/ivabs/install/python_setup`.






Installation
----------------

..  toctree::
    :maxdepth: 1
    
    install/windows
    install/linux
