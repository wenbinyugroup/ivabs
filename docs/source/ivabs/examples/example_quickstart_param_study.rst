.. include:: /replace.txt

.. _section-ivabs_example_quickstart_param_study:

Parameter study of a single cross-section
=============================================

Problem description
-------------------

This example carries out a simple parameter study of a single cross-section by varying two design variables.
The base design of this cross-section has an airfoil profile with a main box-type spar, which is typically seen in helicopter rotor blades.
Here, a template of this type of design is used (``airfoil_gbox_uni.xml.tmp``), which is provided along with the iVABS package.
Two parameters, :math:`a^{wl}_2` and :math:`a^{wt}_2`, control the locations of the front and back spar webs, as shown in :numref:`Fig. %s <fig-ivabs_ex_quickstart_cs_geo_params>`.


..  figure:: /figures/ivabs_ex_quickstart_cs_geo_params.png
    :name: fig-ivabs_ex_quickstart_cs_geo_params
    :width: 6in
    :align: center

    Geometric parameters of the airfoi box-spar baseline design.

The leading web location :math:`a^{wl}_2` is varied from 0.8 to 0.9.
The trailing web location :math:`a^{wt}_2` is varied from 0.5 to 0.6.

Three beam properties are inspected in this example: torsional stiffness :math:`GJ`, flap-wise bending stiffness :math:`EI_f`, and chord-wise bending stiffness :math:`EI_c`.









Main input file setup
----------------------

The main input file ``uh60_blade.yml`` has most of the inputs to the problem.
Descriptions of the complete list of the input files can be found in the section :ref:`section-ivabs_ex_quickstart_files` below.

This section gives a brief explaination of the example main input file, focusing on the overall data layout and several key input specifically related to this problem.

More detailed guide to the configuration of the main input file can be found in :ref:`section-input_guide`.


Overall, the main input file contains the following blocks, as shown in :numref:`Listing %s <code-ivabs_ex_quickstart_param_study_main>`: name, version, setting, design, model, analysis, and study.
The last four are important and hence briefly explained in the following paragraphs.

..  code-block:: yaml
    :caption: Main input file layout.
    :name: code-ivabs_ex_quickstart_param_study_main

    name: "composite_blade_design"
    version: "0.6"
    setting:
        # setting block
    design:
        # design parameter block
    model:
        # model block
    analysis:
        # analysis steps block
    study:
        # design study block

Design block
~~~~~~~~~~~~

In this block, users need to specify the structure that will be studied and provide specific values for design parameters.
For this example, the ``cs`` (standing for cross-section) type structure is studied::

  structure_class: "cs"

Then a list of parameters are used to define a cross-section.
The most important keyword is ``base_design``, indicating the base design template name that will be used::

  base_design: "airfoil_gbox_uni.xml.tmp"

This template has all information needed for PreVABS to create the meshed cross-section.
Some of the inputs in this file are marked with tokens and treated as design parameters that can be varied by Dakota.
Some of them have default values if there is no input from the main input file.
However, for those that do not have default values, such as airfoil name, material/lamina names, etc., users need to specify them in this block.

Every keyword other than ``base_design`` below ``list`` is a token in the template file.
Values after the keywords will be used to substitute the corresponding token during each iteration of the parameter study.

Meanings of the keywords/tokens can be found in section :ref:`section-ivabs_temp_airfoil_gbox_uni`.

The complete input for this block is shown below.

..  code-block:: yaml

    design:
      - name: "cs_1"
        structure_class: "cs"
        parameters:
          list:
            base_design: "airfoil_gbox_uni.xml.tmp"
            mdb_name: "material_database_us_ft"
            airfoil: "SC1095.dat"
            airfoil_point_direction: -1
            lam_spar_1: "T300 15k/976_0.0053"
            lam_front: "T300 15k/976_0.0053"
            lam_back: "T300 15k/976_0.0053"
            lam_skin: "T300 15k/976_0.0053"
            lam_cap: "Aluminum 8009_0.01"
            mat_nsm: "lead"
            mat_fill_front: "Rohacell 70"
            mat_fill_back: "Plascore PN2-3/16OX3.0"
            mat_fill_te: "Plascore PN2-3/16OX3.0"
            gms: 0.004
            rnsm: 0.001

Model block
~~~~~~~~~~~

In this block users need to specify inputs related with the cross-sectional model and analysis tool.

The actual command of VABS installed is specified in ``solver``::

  solver: "VABS"

The actual command of PreVABS installed is specified as, for different operating systems,::

  prevabs_cmd_win: "prevabs.exe"
  prevabs_cmd_linux: "prevabs"

The complete input for this block is shown below.

..  code-block:: yaml

    model:
      cs:
        solver: "VABS"
        prevabs_cmd_win: "prevabs.exe"
        prevabs_cmd_linux: "prevabs"

Analysis block
~~~~~~~~~~~~~~

In this block, users need to provide details of the whole analysis process from design variables to desired outputs, which may contain several steps.

In this example, there is only one step, which is the cross-sectional analysis.
The string after the keyword ``step`` is the name of this step, which can be arbitrary.
It is the following input that tells iVABS that this is a cross-sectional analysis step::

  structure_class: "cs"

Below this, analysis specifications are given for the cross-section ``cs_1``.
Since this example only carries out a direct cross-sectional analysis, we use ``h`` (i.e., homogenization) for the keyword ``analysis``::

  analysis: "h"

All beam properties computed will be read from the VABS output file and stored in the memory.
However, we still need to tell iVABS which properties will be reported to Dakota.
This is specified using the keyword ``final``.
Under this, each beam property returned to Dakota is given a name, in the following format::

  name_for_dakota: "beam_property"

For this example problem, we specify the following::

  cs1_gj: "gj"
  cs1_ei22: "ei22"
  cs1_ei33: "ei33"

The complete input for this block is shown below.

..  code-block:: yaml

    analysis:
      steps:
        - step: "cs analysis"
          structure_class: "cs"
          cs_1:
            settings:
              analysis: "h"
            final:
              cs1_gj: "gj"
              cs1_ei22: "ei22"
              cs1_ei33: "ei33"

Study block
~~~~~~~~~~~

In this block, users need to provide specifications for the parameter study.
Since the builtin MDAO tool is Dakota, this block mainly uses Dakota's keywords and input layout.

Dakota requires the following inputs.

Method
^^^^^^^

For this parameter study example, we choose the ``multidim_parameter_study`` method in Dakota::

  method:
    multidim_parameter_study

The only specification for this method is the number of partitions for each design variable.
For this simple example, we only consider two partitions, i.e., three levels, for each design variable::

  partitions: [2, 2]


Variables
^^^^^^^^^^

This sub-block uses a different layout from Dakota, specified with::

  data_form: "compact"

This arranges the input in a clearer way and makes editing easier than Dakota's format.

As stated in the problem description, we want to vary the leading and trailing webs locations.
They are specified as continuous design variables with the design range [0.8, 0.9] and [0.5, 0.6], respectively::

  data: |
    a2p1,    design, continuous,      0.8:0.9
    a2p3,    design, continuous,      0.5:0.6


Interface
^^^^^^^^^^

This sub-block tells Dakota how to correctly link to the cross-sectional ananlysis.
One important piece of information is a list of files needed to run the cross-sectional analysis.
For this example, this list includes the base design template, the material database, and the airfoil data file.
The are given under the keyword ``required_files``::

  required_files:
    - "airfoil_gbox_uni.xml.tmp"
    - "material_database_us_ft.xml"
    - "SC1095.dat"

Responses
^^^^^^^^^^

This sub-block specifies the quantities of interest for this parameter study, which are the three beam properties requested in the ``analysis`` block.
Same as the ``variables`` sub-block, this input also uses the ``compact`` form of data::

  data: |
    cs1_gj, response
    cs1_ei22, response
    cs1_ei33, response


The complete input for this block is shown below.

..  code-block:: yaml

    study:
      method:
        multidim_parameter_study:
          partitions: [2, 2]
      variables:
        data_form: "compact"
        data: |
          a2p1,    design, continuous,      0.8:0.9
          a2p3,    design, continuous,      0.5:0.6
      interface:
        fork:
          parameters_file: "input.in"
          results_file: "output.out"
          file_save: on
          work_directory:
            directory_tag: on
            directory_save: on
          required_files:
            - "airfoil_gbox_uni.xml.tmp"
            - "material_database_us_ft.xml"
            - "SC1095.dat"
      responses:
        data_form: "compact"
        data: |
          cs1_gj, response
          cs1_ei22, response
          cs1_ei33, response









.. _section-ivabs_ex_quickstart_files:

Files for this example
------------------------

Input files
~~~~~~~~~~~

``airfoil_gbox_uni.xml.tmp``
    This is the design template for the type of cross-section having an airfoil profile with a main box-type spar. Depending on the problem, one or more design templates might be needed. More details on design templates can be found in Section :ref:`section-cs-templates`.

``material_database_us_ft.xml``
    This is the material database used by the cross-section. More details on the material inputs can be found in Section :ref:`section-material-layup`.

``SC1095.dat``
    This is the airfoil data file for the cross-section. Depending on the problem, one or more airfoil data files might be needed. 

``cs_param_study.yml``
    This is the main input file required for all cases. It contains most of the information needed. More details on the main input file can be found in Section :ref:`section-input_guide`.

``run.py``
    This is the startup script. It is required for all cases, but no changes needed and can be directly copied to a different working directory.


.. _section-start_file_out:

Output files
~~~~~~~~~~~~

Current version of iVABS uses Dakota as the driver. Hence, most output files are related to Dakota.

``cs_param_study.dakota``
    This is the Dakota input generated by iVABS from ``cs_param_study.yml``.

``cs_param_study.out``
    This is the Dakota main output file including a summary of the process.

``cs_param_study.results.txt``
    This is the Dakota result file. Contents could be different for different Dakota methods.

``cs_param_study_tabular.dat``
    This contains a table of inputs and outputs of each evaluation/iteration.

``cs_param_study.rst``
    This is the Dakota restart file.
    If the Dakota process stops for some reason, you can try to continue the process from the stopping point, using the following command::

        dakota -i cs_param_study.dakota -read_restart cs_param_study.rst

``cs_param_study.err``
    This is the Dakota error file.

``evals/eval.#/``
    Each directory contains all input and output files for each evaluation/iteration. Links for the five input files are also generated in these directories.

