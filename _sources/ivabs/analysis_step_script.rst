.. highlight:: python

.. _section-guide_analysis_script:


Custom Python Script for Analysis
===================================


The custom scripts provide users the flexibility to do calculations for special purposes that cannot be achieved using built-in functionalities in iVABS.
Typical usages of this include the pre- and post-processing of inputs and outputs of an analysis step.









Prepare the custom scripts
----------------------------------

The script file can be stored anywhere in the system.
There can be multiple functions in the file and they can be named arbitrarily.
However, there are some rules that users should follow when writing the functions so that they can be correctly called in the analysis workflow in iVABS.

..  note::

    These rules only apply to the functions that will be directly linked with iVABS.
    Users can still write functions freely if they are used only by other functions in the custom script, instead of iVABS.

The functions must have the following input list (names of the input variabels can be arbitrary):

..  code-block:: python

    def my_function(ivabs_data, structure_name, logger, *args, **kwargs):

        ...

From the first input variable to the last:

``ivabs_data``
    The core data used by iVABS.

``structure_name``
    The structure or cross-section name of the current analysis step.

``logger``
    The logger object for generating logging information.

``*args``
    Extra positional arguments provided by the user in the main input file.

``**kwargs``
    Extra keyword arguments provided by the user in the main input file.

The key to the communication between a custom function and iVABS is following two aspects:

* how to get needed data from iVABS, and
* how to send calculated result back to iVABS.

Both are done throught the data object ``ivabs_data``.
This is a Python dictionary object and its data layout is:

..  code-block:: python

    ivabs_data = {
        'structures': {
            'blade': ['blade_name_1', ...],
            'cs': ['cs_name_1', 'cs_name_2', ...]
        },
        'blade_name_1': {},
        'cs_name_1': {},
        'cs_name_2': {},
        ...
        'dakota': {}
    }

In this data object:

``structures``
    Names of the blade and cross-sections.
    No matter that cross-sections are predefined explicitly in the main input file or generated during analysis, ``ivabs_data['structures']['cs']`` stores the names of all cross-sections.

``blade_name_1``, ``cs_name_1``, ``cs_name_2``, ...
    Data for each blade and cross-section object.

``dakota``
    Data exchanged between Dakota methods (e.g., parametric study or optimization) and the structural design and analysis.
    Dakota will look for needed results in this key only.


Example 1: Preproess of parameters before cross-sectional analysis
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Suppose that there are two design variables "a" and "b" used by Dakota declared in the main input file.
However, the real design parameter labeled in the cross-sectional template is "c", which is defined as the average of "a" and "b".
Then, for the cross-sectional analysis of each iteration, we need to calculate "c" using "a" and "b" before the substitution of parameters.
This can be done using a custom function as following.

..  code-block:: python

    def calcParamC(ivabs_data, structure_name, logger, *args, **kwargs):
        a = ivabs_data[structure_name]['a']
        b = ivabs_data[structure_name]['b']
        c = (a + b) / 2
        ivabs_data[structure_name]['c'] = c

The value passed to the argument ``structure_name`` from iVABS will always be the name of current cross-section that is going to be analyzed.


Example 2: Postprocess of analysis results for calculating final objectives
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Suppose that we are dealing with a blade analyzed using 10 cross-sections.
The design goal here is to maximize the torsional stiffness GJ.
Specifically, assume the optimization objective is to maximize the minimum GJ among all cross-sections.
The objective required by Dakota is ``gj_min``, declared in the main input file.
This can be done using a custom function as following.

..  code-block:: python

    def calcMinGJ(ivabs_data, structure_name, logger, *args, **kwargs):
        gj_list = []
        for cs_name in ivabs_data['structures']['cs']:
            gj = ivabs_data[cs_name]['gj']
            gj_list.append(gj)
        gj_min = min(gj_list)
        ivabs_data['dakota']['gj_min'] = gj_min









.. _section-guide_analysis_script_main_input:

Include the custom scripts in the main input file
---------------------------------------------------------

Consider the following arrangement of directory and files for a design study:

..  code-block::

    main_input.yml
    my_scripts/
        my_functions.py

and consider the following functions in ``my_functions.py`` that will be used in the analysis:

..  code-block:: python

    def csPreProcess1(ivabs_data, structure_name, logger, *args, **kwargs):
        # Called before a cross-sectional analysis
        # Can be used for preprocessing cross-sectional parameters
        ...

    def csPreProcess2(ivabs_data, structure_name, logger, *args, **kwargs):
        # Called before a cross-sectional analysis
        # Can be used for preprocessing cross-sectional parameters
        ...

    def csPostProcess(ivabs_data, structure_name, logger, *args, **kwargs):
        # Called after a cross-sectional analysis
        # Can be used for postprocessing cross-sectional analysis outputs
        ...

    def finalProcess(ivabs_data, structure_name, logger, *args, **kwargs):
        # Called as a single analysis step
        # Can be used for calculating the final objectives and constraints after all analysis steps
        ...

To let iVABS call these functions properly, the main input file should be configured in the following way (other inputs are omitted and represented using "..."):

..  code-block:: yml

    setting:
      data_process_functions_file: "my_functions"
      ...

    ...

    analysis:
      steps:
      - ...
      - step: "cs analysis"
        structure_class: "cs"
        all:
          preprocess:
          - function: "csPreProcess1"
            args:
            - ...
            kwargs:
              ...
          - function: "csPreProcess2"
          postprocess:
          - function: "csPostProcess"
      - ...
      - step: "final data process"
        type: "script"
        function: "finalProcess"
        args:
        - 1
        - 2
        kwargs:
          a: 11
          b: 22

    study:
      ...
      interface:
        required_files:
        - "my_scripts/my_functions.py"
        - ...


