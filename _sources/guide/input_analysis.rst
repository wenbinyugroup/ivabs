.. highlight:: yaml

.. _section-input_guide_analysis:

Analysis Steps
==============

This block specifies the analysis details that will be carried out during each iteration.
If treated as a black box, the whole analysis process takes two sets of data as the input, one is the set of general design parameters and the other one is the set of specific values of design variables generated during each iteraion.
The outputs are the quantities specified in the ``responses`` block.
The overall layout is shown in :numref:`Listing %s <lst-input_analysis_layout>`.


..  code-block:: yaml
    :name: lst-input_analysis_layout
    :caption: Layout of the analysis input block

    analysis:
      settings:
        ...
      steps:
        - step: "step 1"
          ...
        - step: "step 2"
          type: "script"
          ...
        - ...


The whole analysis process is composed of a list of steps, which will be executed sequentially.
For each step, there are common inputs and special inputs depending on the analysis type.

One common input is the step name::

  step: "The first step"

The name can be arbitrary.
It will mainly be used in logging messages.

Another one the analysis type::

  type: "..."

Supported types are ``built-in`` (default) and ``script``.


Built-in analysis type (``type: "built-in"``)
-------------------------------------------------

This type is mainly for structural analyses such as cross-sectional analysis.
Since different structures could have different treatment in an analysis, this type of analysis step is further classified into subgroups.
iVABS supports two classes of structures: blade (``blade``) and cross-section (``cs``).
Specifications for the analysis step are provided for each or all structures defined in the ``design`` block or generated during previous steps.
A template is given in :numref:`Listing %s <lst-input_analysis_builtin>`.

..  code-block:: yaml
    :name: lst-input_analysis_builtin
    :caption: Layout of the analysis step of the built-in type

    - step: "structural analysis"
      structure_class: "blade" # or "cs"
      all:  # or a specific structure name
        settings:
          ...
        inputs:
          ...
        preprocess:
          - function: "prep1"
          ...
        postprocess:
          - function: "postp1"
          ...
        outputs:
          ...

``settings`` specifies configurations for the current analysis step.
``inputs`` specifies any extra data needed by this step besides those already given at other places in the input file.
``preprocess`` specifies functions that will process data before running the actual analysis.
``postprocess`` specifies functions that will process data after running the analysis.
``outputs`` specifies quantities that will be the output of the analysis and may be inputs to the next step.


Blade class (``structure_class: "blade"``)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This class mainly serves the purpose of generating designs of cross-sections from the blade design.
This is specified by set ``analysis`` to ``1``.
The input required is a list of locations along the blade span indicating the cross-sections that will be generated and analyzed.

..  code-block:: yaml

    - step: "generate cs design"
      structure_class: "blade"
      blade_name:
        settings:
          analysis: 1
        inputs:
          stations: [0.1, 0.5, 0.9]

..  note::

    Pay attention to keep the units used here and the those used in the design block consistent.




Cross-section class (``structure_class: "cs"``)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This class is mainly responsible for the cross-sectional analysis such as calculating beam properties and failure analysis.

Analysis of beam properties
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Set ``analysis`` to ``"h"`` to calculate the beam properties.

..  code-block:: yaml

    - step: "calc beam properties"
      structure_class: "cs"
      cs_name:  # or "all"
        settings:
          analysis: "h"
          timeout: 30
        ...

``timeout`` under ``settings`` can be used to set a limit to the running time of this step.
The purpose is to kill the process of PreVABS if the code is stuck because of infeasible designs.
Custom functions can be added under ``preprocess`` to process the input before sending to PreVABS.


Analysis of initial failure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Set ``analysis`` to ``"fi"`` to carry out the failure analysis.

..  code-block:: yaml

    - step: "failure analysis"
      structure_class: "cs"
      cs_name:  # or "all"
        settings:
          analysis: "fi"
        inputs:
          load_cases:
            ...

For this analysis, sectional loads should be provided as the extra inputs (``load_cases``).
Currently the accepted form of providing loads is through a load file (``data_form: "file"``) and the supported format is CSV (``data_format: "csv"``).
Name of the load file is provided at ``file_name``.

..  code-block:: yaml

    load_cases:
      data_form: "file"
      data_format: "csv"
      file_name: "load.csv"
      flight_condition: 1
      azimuth: 90

Currently iVABS mainly considers the use cases for helicopter rotors.
Hence, loads can be provided for different flight conditions and azimuth angles.
Desired flight condition and azimuth angles for which the failure analysis will be carried out can be specified at ``flight_condition`` and ``azimuth``, respectively.
Multiple loading conditions can be given here::

  flight_condition: [1, 2, 3]
  azimuth: [0, 90, 180, 270]

A sample file storing the sectional loads is shown in  :numref:`Listing %s <lst-input_analysis_cs_fi_load_file>`.
The first row is the column names.
Each set of loads (six components) should have corresponding condition number, azimuth angle (``phi``), and spanwise location (``r``).

..  code-block::
    :name: lst-input_analysis_cs_fi_load_file
    :caption: Sample file for sectional loads.

    condition,phi,r,Fx,Fy,Fz,Mx,My,Mz
    1,0,0.1,1,2,3,4,5,6
    1,0,0.5,7,8,9,10,11,12
    1,0,0.9,13,14,15,16,17,18
    1,90,0.1,19,20,21,22,23,24
    1,90,0.5,25,26,27,28,29,30
    1,90,0.9,31,32,33,34,35,36
    ...


Custom analysis type (``type: "script"``)
----------------------------------------------

This type is for executing any custom Python scripts.
A common case of using this type is the calculation of objectives and constraints in optimizations, since such calculations are usually problem dependent.

..  code-block:: yaml
    :name: lst-input_analysis_step_script
    :caption: Layout of the analysis step of custom script

    - step: ""
      type: "script"
      function: "my_function"
      args:
        - arg1
        - arg2
        ...
      kwargs:
        kw1: kwarg1
        kw2: kwarg2
        ...

Keyword ``function`` specifies the name of the Python function that will be executed.
All inputs under ``args`` and ``kwargs`` will be passed to ``*args`` and ``**kwargs`` of the function, respectively.

..  note::

    The guide to writing custom Python scripts that can be linked to iVABS can be found in Section :ref:`section-guide_analysis_script`.


