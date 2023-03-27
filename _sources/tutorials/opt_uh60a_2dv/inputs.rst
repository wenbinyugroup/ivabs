Preparation of Input Files
==========================

This optimization study requires the following files as the inputs.

.. list-table:: Input files
    :align: center
    :header-rows: 1

    * - File name
      - Description
    * - ``uh60a_section.xml.tmp``
      - Cross-sectional design template
    * - ``material_database.xml``
      - Material database
    * - ``sc1095.dat``
      - Airfoil data
    * - ``interface.py``
      - Interface for Dakota to run the analysis
    * - ``interface_args.json``
      - Arguments for the analysis
    * - ``data_proc_funcs.py``
      - Functions for processing data (input/output)
    * - ``cs_tm_opt_soga.dakota``
      - Dakota input file; Specify optimization study setup


.. toctree::
    :maxdepth: 2
    :caption: Contents:
  
    inputs_cs_template
    inputs_cs_materials
    inputs_cs_airfoil
    inputs_interface
    inputs_arguments
    inputs_data_process
    inputs_dakota

