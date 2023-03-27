.. _section-install:

Download and Installation
=========================

Prerequisites
-------------

Download and install VABS 4.0 (with valid license).
In the instructions below, ``VABS_DIR`` refers to the path to the VABS executable.
VABS manual can be found and downloaded here [VABS]_.

Download and install Gmsh (http://gmsh.info/) following the official
instructions. In the instructions below, ``GMSH_DIR`` refers to the
path to the Gmsh executable.

Install binary
--------------

Download PreVABS binary from cdmHUB (https://cdmhub.org/resources/1597/supportingdocs).
Unpack the package to any location. In the instructions below,
``PREVABS_DIR`` refers to the path to the PreVABS executable;

Add those paths to executables to the system environment variable ``PATH``;

- On Windows:

  Open Environment Variables editor. Edit user variables for your account
  or edit system variables if you have the administrator access. Add
  ``VABS_DIR``, ``GMSH_DIR``, and ``PREVABS_DIR`` to the variable ``PATH``.

- On Linux:

  In the shell, type::

    export PATH=$VABS_DIR:$GMSH_DIR:$PREVABS_DIR:$PATH

  To make this effective each time starting the bash, you can add this
  command to the bash startup file, which may be ``~/.bashrc``,
  ``~/.bash_profile``, ``~/.profile``, or ``~/bash_login``;

.. Build from source
.. -----------------
