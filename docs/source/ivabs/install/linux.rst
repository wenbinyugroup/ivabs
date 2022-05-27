Installation on Linux
======================

..  note::

    In the instructions below ``IVABS_ROOT`` refers to the root directory of iVABS after installation.









Installer (``ivabs-#.#-linux-installer.sh``)
---------------------------------------------

#.  Run

    ..  code-block:: bash

        bash ivabs-#.#-linux-installer.sh

#.  Select the installation directory of your own choice. The default is ``ivabs`` inside your home directory, i.e. ``IVABS_ROOT=$HOME/ivabs``.
#.  If you already have Dakota already installed on your computer, you can skip Dakota installation by answering ``no`` to that question. 
#.  Environment variables of ``PATH``, ``LD_LIBRARY_PATH`` and ``PYTHONPATH`` can be updated automatically (wrote to the shell startup file such as ``.bash_profile``). However, if your shell/terminal uses a different startup file such as ``.bashrc``, you can set these environmental variables by yourself. 




Portable archive (``ivabs-#.#-linux-portable.tar.gz``)
--------------------------------------------------------

#. Unpackage the archive to a directory of your own choice. For example, you can use the following command to install iVABS in $HOME/ivabs.

   .. code-block:: bash

      tar xzvfC ivabs_#.#_linux_portable.tar.gz $HOME

#. Set environment variables manually. For example, for bash shell, you can use the following commands to set the environment variables for the current shell session.

   ..  code-block:: bash

    export PATH=$IVABS_ROOT/bin:$PATH
    export LD_LIBRARY_PATH=$IVABS_ROOT/bin:$LD_LIBRARY_PATH
    export PYTHONPATH=$IVABS_ROOT/scripts:$PYTHONPATH

    # If the Dakota included in the iVABS release is installed
    export PATH=$IVABS_ROOT/dakota/bin:$PATH
    export PYTHONPATH=$IVABS_ROOT/dakota/share/dakota/Python:$PYTHONPATH

    If you want to make this setting permanent, you need to add the above commands to the startup file of the shell. Typical startup files for bash shells are ``~/.bashrc`` or ``~/.bash_profile``. After editing and saving the startup file, use the following command in the shell to activate these changes:

    ..  code-block:: bash

    source ~/.bash_profile  # or other startup file
