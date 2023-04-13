.. highlight:: python

.. _section-guide_analysis_script:

Custom script analysis step
============================



The custom scripts provide users the flexibility to do calculations for special purposes that cannot be achieved using built-in functionalities in |msgd|.
Typical usages of this include the pre- and post-processing of inputs and outputs of an analysis step.









Prepare the custom scripts
----------------------------------

The script file can be stored anywhere in the system.
There can be multiple functions in the file and they can be named arbitrarily.
However, there are some rules that users should follow when writing the functions so that they can be correctly called in the analysis workflow in |msgd|.

..  note::

    These rules only apply to the functions that will be directly linked with |msgd|.
    Users can still write functions freely if they are used only by other functions in the custom script, instead of |msgd|.

The functions must have the following input list (names of the input variabels can be arbitrary):

..  code-block:: python

    def my_function(data, sname, logger, *args, **kwargs):

        ...

From the first input variable to the last:

``data``
    The core data used by |msgd|.

``sname``
    The structure or cross-section name of the current analysis step.

``logger``
    The logger object for generating logging information.

``*args``
    Extra positional arguments provided by the user in the main input file.

``**kwargs``
    Extra keyword arguments provided by the user in the main input file.

The key to the communication between a custom function and |msgd| is following two aspects:

* how to get needed data from |msgd|, and
* how to send calculated result back to |msgd|.

Both are done throught the data object ``data``.
This is a Python dictionary object and its data layout is:

.. only:: msg

    ..  code-block:: python

        data = {
            'main': {
                'mdao_design_variable_1': dv_value_1,
                'mdao_design_variable_2': dv_value_2,
                ...
                'mdao_design_response_1': dr_value_1,
                'mdao_design_response_2': dr_value_2,
                ...
            }
            'structure': {
                'design': {
                    'parameters': {}
                },
                'sgs_data': {
                    'sg1': {}
                }
            },
            'sgdb': {},
        }


.. only:: ivabs

    ..  code-block:: python

        data = {
            'main': {
                'mdao_design_variable_1': dv_value_1,
                'mdao_design_variable_2': dv_value_2,
                ...
                'mdao_design_response_1': dr_value_1,
                'mdao_design_response_2': dr_value_2,
                ...
            }
            'structure': {
                'parameter': {},
                'design': {},
                'css_data': {
                    'cs_set1': {
                        'parameter': {},
                        'property': {
                            'md1': {
                                ...
                            }
                        }
                    },
                    'cs_set2': {},
                    ...
                }
            },
            'csdb': {},
        }


In this data object:

``main``
    Data exchanged between Dakota methods (e.g., parametric study or optimization) and the structural design and analysis.
    Dakota will look for needed results in this key only.

``structure``
    All data related with the structure.

.. ``blade_name_1``, ``cs_name_1``, ``cs_name_2``, ...
..     Data for each blade and cross-section object.

``sgdb``
    SG database.

..  only:: ivabs

    ..  note::

        This data object is written into three files (``msgd.data.yml``, ``msgd.structure_data.yml``, and ``cs_db.yml``) as interim output in the same folder as the main input file.
        Users can always check these files for more details.

    ..  note::

        More details on the available beam properties can be found in :ref:`section-beam_properties`.


Examples
------------

..

    Example 1: Preproess of parameters before cross-sectional analysis
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    Suppose that there are two design variables "a" and "b" used by Dakota declared in the main input file.
    However, the real design parameter labeled in the cross-sectional template is "c", which is defined as the average of "a" and "b".
    Then, for the cross-sectional analysis of each iteration, we need to calculate "c" using "a" and "b" before the substitution of parameters.
    This can be done using a custom function as following.

    ..  code-block:: python

        def calcParamC(data, structure_name, logger, *args, **kwargs):
            a = data[structure_name]['a']
            b = data[structure_name]['b']
            c = (a + b) / 2
            data[structure_name]['c'] = c

    The value passed to the argument ``structure_name`` from iVABS will always be the name of current cross-section that is going to be analyzed.


#. Postprocess of analysis results for calculating final objectives
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Suppose that we are dealing with a blade analyzed using 10 cross-sections.
The design goal here is to maximize the torsional stiffness GJ.
Specifically, assume the optimization objective is to maximize the minimum GJ among all cross-sections.
The objective required by Dakota is ``gj_min``, declared in the main input file.
This can be done using a custom function as following.

..  code-block:: python

    def calcMinGJ(data, sname, logger, *args, **kwargs):
        gj_list = []
        for _cs_name, _cs_data in data['structure']['css_data'].items():
            gj = _cs_data['property']['md1']['gj']
            gj_list.append(gj)
        gj_min = min(gj_list)
        data['main']['gj_min'] = gj_min









.. _section-guide_analysis_script_main_input:

Include the custom scripts in the main input file
---------------------------------------------------------

Consider the following arrangement of directory and files for a design study:

..  code-block::

    main_input.yml
    my_scripts/
        my_functions.py

and consider the following functions in ``my_functions.py`` that will be used in the analysis:

..  only:: msg

    ..  code-block:: python

        def csPreProcess1(data, sname, logger, *args, **kwargs):
            # Called before a cross-sectional analysis
            # Can be used for preprocessing cross-sectional parameters
            ...

        def csPreProcess2(data, sname, logger, *args, **kwargs):
            # Called before a cross-sectional analysis
            # Can be used for preprocessing cross-sectional parameters
            ...

        def csPostProcess(data, sname, logger, *args, **kwargs):
            # Called after a cross-sectional analysis
            # Can be used for postprocessing cross-sectional analysis outputs
            ...

        def finalProcess(data, sname, logger, *args, **kwargs):
            # Called as a single analysis step
            # Can be used for calculating the final objectives and constraints after all analysis steps
            ...


..  only:: ivabs

    ..  code-block:: python

        def finalProcess(data, sname, logger, *args, **kwargs):
            # Called as a single analysis step
            # Can be used for calculating the final objectives and constraints after all analysis steps
            ...
            subProcess()
            ...


        def subProcess():
            ...



To let |msgd| call these functions properly, the main input file should be configured in the following way (other inputs are omitted and represented using "..."):

..  only:: msg

    ..  code-block:: yaml

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



..  only:: ivabs

    ..  code-block:: yaml

        ...

        analysis:
            steps:
              - ...
              - step: "final data process"
                type: "script"
                file: "my_scripts"
                function: "finalProcess"
                args:
                    - 1
                    - 2
                kwargs:
                    a: 11
                    b: 22
              - ...

        study:
          ...
          interface:
            required_files:
              - "my_scripts/my_functions.py"  # or "my_scripts/*"
              - ...

