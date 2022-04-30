Installation on Linux
======================

Below ``IVABS_ROOT`` stands for the root directory of iVABS after installation.

Installer (``ivabs-#.#-linux-installer.sh``)
---------------------------------------------

#. Run

   .. code-block:: bash

      bash installer.sh

#. Select the installation folder of your own choice. The default folder is ``ivabs`` inside your home folder, i.e. ``IVABS_ROOT=~/ivabs``.
#. Dakota is optional. If you would like to continue use the Dakota already installed on your computer, you need to uncheck the option.
#. Environment variables of PATH and PYTHONPATH can be updated automatically (write to ``.bashrc`` or ``.zshrc`` file). However, if your linux box using a different shell startup file such as ``.bash_profile``, you can set these environmental variables by yourself. 


Portable archives (``ivabs-#.#-linux-portable.tar.gz``)
--------------------------------------------------------

#. Uncompress the archive to a folder of your own choice.

   .. code-block:: bash

      tar xzvf ivabs_#.#_linux_portable.tar.gz

#. Set environment variables manually.


Setting environment variables
------------------------------

Add the following directories to ``PATH``:

- ``IVABS_ROOT/bin``
- ``IVABS_ROOT/dakota/bin`` (required only if the Dakota delivered with iVABS is used)

Add the following directory to ``LD_LIBRARY_PATH``:

- ``IVABS_ROOT/bin``

Add the following directories to ``PYTHONPATH``:

- ``ivabs/scripts``
- ``ivabs/dakota/share/dakota/Python`` (required only if the Dakota delivered with iVABS is used)



