Download and Installation
=========================

iVABS can be dowloaded from `its Release Page on github <https://github.com/wenbinyugroup/ivabs/releases>`_. Installer contains a single executable for installation while Portable Archive contains all the files in an archive which should be extracted for installation.  

Windows installer
-----------------
#. Select the installation folder of your own choice. The default folder is ``iVABS`` inside your home folder. You should have writing permission for the folder to install iVABS. 
#. Dakota is optional. If you would like to continue use the version of Dakota you already have on your computer, you need to uncheck the option. However, you need to make sure that Dakota binary and Dakota python library are available in the Path. 
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
  #. Select the installation folder of your own choice. The default folder is ``iVABS`` inside your home folder.
  #. Dakota is optional. If you would like to continue use the version of Dakota you already have on your computer, you need to uncheck the option. However, you need to make sure that Dakota binary and Dakota python library are available in the Path. 
  #. Environment variables of PATH and PYTHONPATH can be updated automatically (write to ``.bashrc`` or ``.zshrc`` file). However, if your linux box using a different file such as .bash_profile for storing these variables, you can set these environmental variables by yourself. 
    - ``ivabs\bin`` should be in **PATH**. 
    - ``ivabs\vendors\dakota\share\dakota\Python`` should be in **PYTHONPATH**. Use the corresponding Dakota Python PATH if you want to use the Dakota already installed on your computer.
    - ``ivabs\vendors\msgpi`` should be in **PYTHONPATH**.
  5. Python3 is needed for using MSGPI. Necessary Python packages include: ``numpy, matplotlib``.
  6. After installation, inside ``ivabs``, there are six folders. The ``vendors`` folder contains all the codes integrated in iVABS. The ``bin`` folder contains shortcuts to the executables of different codes in ``vendors``. If you want to use the Dakota already installed on your computer. please delete the shortcut ``dakota`` inside the ``bin`` folder. 

Linux portable archives
-----------------------
  #. Uncompress the archive using ``tar xzvf ivabs_x.x_linux64_portable.tar.gz`` to a folder of your own choice. 
  #. Environment variables of PATH and PYTHONPATH should be added manually. 
    - ``ivabs\bin`` should be in **PATH**. Delete the ``dakota" shortcut inside ``bin`` if you want the Dakota already installed on your computer. 
    - ``ivabs\vendors\dakota\share\dakota\Python`` should be in **PYTHONPATH**. Use the corresponding Dakota Python PATH if you want to use the Dakota already installed on your computer.
    - ``ivabs\vendors`` should be in **PYTHONPATH**.


Request VABS license
--------------------
VABS is a commercial code distributed along with iVABS. However, you need to request a license from `AnalySwift <http://analyswift.com/software-trial/>`_.
Put the license file in ``ivabs``.

