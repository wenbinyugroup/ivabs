Installation on Windows
========================

``IVABS_ROOT`` refers to the root directory of iVABS after installation.

Installer (``ivabs-#.#-windows-installer.exe``)
------------------------------------------------

#. Select the installation directory of your own choice. The default directory is ``iVABS`` inside your home directory. You should have writing permission for the direcotry to install iVABS. 
#. Dakota is optional. If you would like to continue use the version of Dakota you already have on your computer, you need to uncheck the option. However, you need to make sure that Dakota binary and Dakota python library are available in the Path. 
#. Environment variables of **PATH** and **PYTHONPATH** can be updated automatically. This is needed if you want to use iVABS toolset from the command prompt.
#. A shortcut can be created in the Start Menu and Desktop.


Portable archive (``ivabs-#.#-windows-portable.7z``)
-----------------------------------------------------

#. Extract the archive to a directory of your own choice. 
#. Use the embeded ``env.cmd`` to automatically set up environment variables, or set up environment variables manually according to ``env.cmd``. Specifically, you need to add the following directories to ``PATH``:

   - ``IVABS_ROOT/bin``
   - ``IVABS_ROOT/dakota/bin`` (required only if the Dakota included in the iVABS release is used)

   and the following directories to ``PYTHONPATH``:

   - ``ivabs/scripts``
   - ``ivabs/dakota/share/dakota/Python`` (required only if the Dakota included in the iVABS release is used)

