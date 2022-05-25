Installation on Linux
======================

..  note::

    In the instructions below ``$IVABS_ROOT`` refers to the root directory of iVABS after installation.









Installer (``ivabs-#.#-linux-installer.sh``)
---------------------------------------------

#.  Run

    ..  code-block:: bash

        bash installer.sh

#.  Select the installation folder of your own choice. The default folder is ``ivabs`` inside your home folder, i.e. ``IVABS_ROOT=~/ivabs``.
#.  Dakota is optional. If you would like to continue use the Dakota already installed on your computer, you need to uncheck the option.
#.  Environment variables of PATH and PYTHONPATH can be updated automatically (write to ``.bashrc`` or ``.zshrc`` file). However, if your linux box using a different shell startup file such as ``.bash_profile``, you can set these environmental variables by yourself. 




Portable archives (``ivabs-#.#-linux-portable.tar.gz``)
--------------------------------------------------------

#. Uncompress the archive to a folder of your own choice.

   .. code-block:: bash

      tar xzvf ivabs_#.#_linux_portable.tar.gz

#. Set environment variables manually.









Set environment variables
-------------------------

The following scripts can set the environment variables for the current shell session.

If you want to make this setting permanent, the following scripts need to be added to the startup file of the shell you use.


Bash shell
~~~~~~~~~~

..  code-block:: bash

    export PATH=$IVABS_ROOT/bin:$PATH
    export LD_LIBRARY_PATH=$IVABS_ROOT/bin:$LD_LIBRARY_PATH
    export PYTHONPATH=$IVABS_ROOT/scripts:$PYTHONPATH

    # If built-in Dakota is needed
    export PATH=$IVABS_ROOT/dakota/bin:$PATH
    export PYTHONPATH=$IVABS_ROOT/dakota/share/dakota/Python:$PYTHONPATH


Typical startup files for bash shells can be ``~/.bashrc`` or ``~/.bash_profile``.

After editing and saving the startup file, use the following command in the shell to activate these changes:

..  code-block:: bash

    source ~/.bash_profile  # or other startup file




