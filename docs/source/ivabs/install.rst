Download and Installation
=========================

iVABS can be dowloaded from `its Release Page on github <https://github.com/wenbinyugroup/ivabs/releases>`_. Installer contains a single executable for installation while Portable Archive contains all the files in an archive which should be extracted for installation.  

Windows installer
-----------------
#. Select the installation folder of your own choice. The default folder is ``iVABS`` inside your home folder. You should have writing permission for the folder to install iVABS. 
#. Dakota is optional. If you would like to continue use the version of Dakota you already have on your computer. You need to uncheck the option. However, you need to make sure that Dakota binary and Dakota python library are available in the Path. 
#. Environment variables of **PATH** and **PYTHONPATH** can be updated automatically. This is needed if you want to use iVABS toolset from the command prompt.
#. A shortcut can be created in the Start Menu and Desktop.
#. Python3 is needed for using MSGPI. Necessary Python packages include: ``numpy, matplotlib``.

Windows portable archive
-------------------------
  #. Extract the archive to a folder of your own choice. 
  #. Use the embeded ``env.cmd`` to automatically set up environment variables, or set up environment variables manually according to ``env.cmd``.

Linux installer
---------------
  #. Excute the installer ``bash installer.sh``.
  #. Select your installation path. ``ivabs-folder`` will be used to reference the path.
  #. Dakota is optional. But if you need Dakota(v6.8), you need to make sure Dakota binary and Dakota python library are available in the path;
  #. Environment variables of PATH and PYTHONPATH can be updated automatically (write to ``.bashrc`` or ``.zshrc`` file).
    - ``ivabs-folder\bin`` should be in **PATH**. Delete dakota soft link if you want 
      to use your own Dakota.
    - ``ivabs-folder\vendors\dakota\share\dakota\Python`` should be in **PYTHONPATH**. 
      Use your own Dakota PATH if you want to use your own Dakota.
    - ``ivabs-folder\vendors`` should be in **PYTHONPATH**
  #. Python3 is needed. Necessary python package include: ``numpy, matplotlib``

Linux portable archives
-----------------------
  #. Uncompress the archive: ``tar xJvf iVABS.tar.xz``. Move to your desired folder ``ivabs-folder``.
  #. Environment variables of PATH and PYTHONPATH should be added manually. 

    - ``ivabs-folder\bin`` should be in **PATH**. Delete dakota soft link if you want 
      to use your own Dakota.

    - ``ivabs-folder\vendors\dakota\share\dakota\Python`` should be in **PYTHONPATH**. 
      Use your own Dakota PATH if you want to use your own Dakota.

    - ``ivabs-folder\vendors`` should be in **PYTHONPATH**

  #. Python3 is needed. Necessary python package include: ``numpy, matplotlib``.

Request VABS license
--------------------
VABS is a commercial code distributed along with iVABS. However, you need to request a license from `AnalySwift <http://analyswift.com/software-trial/>`_.
Put the license file in ``ivabs``.

