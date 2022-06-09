Installation on Linux
======================

..  note::

    ``IVABS_ROOT`` refers to the root directory of iVABS after installation.









Installer (``ivabs-#.#-linux-installer.sh``)
---------------------------------------------

#.  Run

    ..  code-block:: bash

        bash ivabs-#.#-linux-installer.sh

#.  Select the installation directory of your own choice. The default is ``ivabs`` inside your home directory, i.e. ``IVABS_ROOT=$HOME/ivabs``.
#.  If you have Dakota already installed on your computer, you can skip Dakota installation by answering ``no`` to that question. 
#.  Environment variables of ``PATH``, ``LD_LIBRARY_PATH`` and ``PYTHONPATH`` can be updated automatically and wrote to the shell startup file. The installer will detect the shell you are currently using and use a default startup file (``.bash_profile`` for bash, ``.zshrc`` for zsh, ``.cshrc`` or ``.tcshrc`` for csh). However, if your shell/terminal uses a different startup file such as ``.bashrc``, you need to set these environmental variables by yourself as described in the next section.
#.  You need to make these changed environment variables effective by using a correspondng command (such as ``source $HOME/.bash_profile`` for bash) or restart the terminal shell.




Portable archive (``ivabs-#.#-linux-portable.tar.gz``)
--------------------------------------------------------
#. Unpackage the archive to a sub-directory called ivabs within the current directory using the following command. 

   .. code-block:: bash

      tar xzvf ivabs_#.#_linux_portable.tar.gz

#. You can also unpackage the archive to a directory of your own choice. For example, you can use the following command to install iVABS in $HOME/ivabs.

   .. code-block:: bash

      tar xzvfC ivabs_#.#_linux_portable.tar.gz $HOME
    
#. Set environment variables manually. For example, for bash shell, you can use the following commands to set the environment variables for the current shell session.

   ..  code-block:: bash

    export PATH=$PATH:$IVABS_ROOT/bin
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$IVABS_ROOT/bin
    export PYTHONPATH=$PYTHONPATH:$IVABS_ROOT/scripts

    # If the Dakota included in the iVABS release is installed
    export PATH=$PATH:$IVABS_ROOT/dakota/bin

#. If you want to make this setting permanent, you need to add the above commands to the startup file of the shell. Typical startup files for bash shells are ``~/.bashrc`` or ``~/.bash_profile``. After editing and saving the startup file, use the following command in the shell to activate these changes:

   ..  code-block:: bash

    source ~/.bash_profile  # or other startup file
