Carry out a single cross-sectional analysis
============================================


This first tutorial will give the instructions to the basic functionalities of the tool.

Suppose that we want to carry out a single cross-sectional analysis.
The task is to carry out a quick cross-sectional analysis of a specific cross-sectional design.
Specifically, in this tutorial, we want to set values to the locations of spar webs and get the torsional and bending stiffness (|gj|, |eiyy|, |eizz|).


Run the example
----------------------

To run the tutorial, start a command line prompt, change directory to this tutorial folder, and run the following command:

..  code-block:: shell

    python run.py cs_design_analysis.yml

Result can be found in the file ``cs_design_analysis.out``.




Files of this tutorial
-----------------------

For this and all analysis of |msgd|, there is one top-level yaml file as the main input and a Python script to trigger the analysis.
All others are the supporting files.

..  list-table:: Tutorial files
    :header-rows: 1

    * - File
      - Description
    * - ``cs_design_analysis.yml``
      - Main input file
    * - ``run.py``
      - Python script running the analysis
    * - ``airfoil_simple.xml.tmp``
      - Cross-sectional design template
    * - ``SC1095.dat``
      - Airfoil data
    * - ``material_database_us_ft.xml``
      - Material database

This tutorial mainly focuses on the main input file.
Tutorials on other files will be explained later.




Main input file specification (``cs_design_analysis.yml``)
------------------------------------------------------------

..  note::

    For more details on the syntax of the YAML format, please see :ref:`section-yaml`.



Basic layout of the main input file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: yaml
    :linenos:

    cs:
      # Define cross-sectional designs

    analysis:
      # Define analysis steps




Define the cross-section
^^^^^^^^^^^^^^^^^^^^^^^^^^

This block specifies the base design of the cross-section that will be analyzed.

..  code-block:: yaml
    :linenos:

    cs:
      - name: "airfoil"
        parameter:
          a2p1: 0.82
          a2p3: 0.58
        design:
          dim: 2
          tool: "prevabs"
          base_file: "airfoil_simple.xml.tmp"
        model:
          md1:
            tool: "vabs"



..  note::

    For more details on how to prepare the parameterized base design of a cross-section (``airfoil_simple.xml.tmp``), please see :ref:`section-ivabs_parameterization`.




Define the analysis
^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: yaml
    :linenos:

    analysis:
      steps:
        - step: "cs analysis"
          type: "cs"
          analysis: "h"
          output:
            - value: ["gj", "eiyy", "eizz"]


..  note::

    For the complete list of available keys to get beam properties, see :ref:`section-beam_properties`.



