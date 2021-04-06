Download and Installation
=========================

iVABS can be dowloaded from `its Release Page on github <https://github.com/wenbinyugroup/ivabs/releases>`_. Installers contain a single executable for installation while Portable Archives contain all the files in an archive which should be extracted for installation. With Portable Archives, one can install iVABS without Administrator privilege. 

Windows installer
-----------------

  1. Select the installation path of your own choice. 

  2. Dakota is optional. But if you need Dakota, you need to make sure Dakota binary and
     Dakota python library are available in the path. 
     
  3. Examples and help files are also optional;

  4. Environment variables of **PATH** and **PYTHONPATH** can be updated automatically; this is
     necessary if you want to use iVABS toolset from any command prompt.

  5. A shortcut can be created in the Start Menu and Desktop, which provides a quick link to the iVABS toolset.

  6. Python3 is needed. Necessary Python package include: ``numpy, matplotlib``.

Windows portable archives
-------------------------

  1. Extract the archive to a folder of your own choice. 

  2. Use the embeded ``env.cmd`` to automatically set up environment variables, or set up environment variables manually according to ``env.cmd``.

Linux installer
---------------

  1. Excute the installer ``bash installer.sh``.

  2. Select your installation path. ``ivabs-folder`` will be used to reference the path.

  3. Dakota is optional. But if you need Dakota(v6.8), you need to make sure Dakota
     binary and Dakota python library are available in the path;
  
  4. Environment variables of PATH and PYTHONPATH can be updated automatically
     (write to ``.bashrc`` or ``.zshrc`` file).

    - ``ivabs-folder\bin`` should be in **PATH**. Delete dakota soft link if you want 
      to use your own Dakota.

    - ``ivabs-folder\vendors\dakota\share\dakota\Python`` should be in **PYTHONPATH**. 
      Use your own Dakota PATH if you want to use your own Dakota.

    - ``ivabs-folder\vendors`` should be in **PYTHONPATH**

  5. Python3 is needed. Necessary python package include: ``numpy, matplotlib``

Linux portable archives
-----------------------

  1. Uncompress the archive: ``tar xJvf iVABS.tar.xz``. Move to your desired folder
     ``ivabs-folder``.

  2. Environment variables of PATH and PYTHONPATH should be added manually. 

    - ``ivabs-folder\bin`` should be in **PATH**. Delete dakota soft link if you want 
      to use your own Dakota.

    - ``ivabs-folder\vendors\dakota\share\dakota\Python`` should be in **PYTHONPATH**. 
      Use your own Dakota PATH if you want to use your own Dakota.

    - ``ivabs-folder\vendors`` should be in **PYTHONPATH**

  3. Python3 is needed. Necessary python package include: ``numpy, matplotlib``.

Request VABS license
--------------------

VABS is a commercial code. Please qequest VABS license from `AnalySwift <http://analyswift.com/software-trial/>`_.
Put the license file in ``ivabs-folder``.

