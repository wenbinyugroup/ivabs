Installation on Windows
========================

Installer (``ivabs-#.#-windows-installer.exe``)
------------------------------------------------

#. Select the installation directory of your own choice. The default directory is ``iVABS`` inside your home directory. You should have writing permission for the direcotry to install iVABS. 
#. Dakota is optional. If you would like to continue use the version of Dakota you already have on your computer, you need to uncheck the option. However, you need to make sure that Dakota binary and Dakota python library are available in the Path. 
#. Environment variables of **PATH** and **PYTHONPATH** can be updated automatically. This is needed if you want to use iVABS toolset from the command prompt.
#. A shortcut can be created in the Start Menu and Desktop.


Portable archive (``ivabs-#.#-windows-portable.zip``)
-----------------------------------------------------

#. Unzip the package to a directory of your own choice.
    
#. Set environment variables manually. This setting will be effective as long as the command line window is open. Please note replace ``IVABS_ROOT`` with the root directory of iVABS. 

   ..  code-block:: shell

       set PATH=%IVABS_ROOT%/bin;%PATH%
       set PYTHONPATH=%IVABS_ROOT%/scripts;%PYTHONPATH%

       # If the Dakota included in the iVABS release is installed
       set PATH=%IVABS_ROOT%/dakota/bin;%PATH%

#. If you want to make this change permanent, you need to edit the environment variable in your system setting. You can try to search the system tool named "Edit environment variables for your account".
