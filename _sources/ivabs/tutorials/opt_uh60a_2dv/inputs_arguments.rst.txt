
.. _sect-input-arguments:

Interface Arguments (``interface_args.json``)
=============================================

This file stores all configurations and arguments that will be used in the interface script.
All arguments can be roughly divided to three groups: general, cross-sectional analysis and post-processing.




.. _sect-input-arguments-general:

General
-------

To control the screen output of preVABS and VABS, use the keyword ``scrnout``::

  "scrnout": false,

To control the level of logging message output, use the following keywords.
``log_level_cmd`` sets the output level to the screen.
``log_level_file`` sets the output level to the log file.
The level can be one of the following: ``debug``, ``info``, ``warning``, ``error``, ``critical``, with logging level increasing from the first to the last.
``log_file_name`` sets the log file name.
::

  "log_level_cmd": "critical",
  "log_level_file": "info",
  "log_file_name": "eval.log",

``data_process_functions_file`` sets the script file name (without file extension) storing data processing functions.
::

  "data_process_functions_file": "data_proc_funcs",

This file will be imported into the analysis script, see moduel loading in Section: :ref:`sect-input-interface-init`.




.. _sect-input-arguments-cs-analysis:

Cross-sectional analysis
------------------------

Corresponding to the cross-sectional analysis step in the interface script (Section: :ref:`sect-input-interface-cs-analysis`), some arguments need to be configured here.

First, names of pre-processing functions are given in a list after the keyword ``cs_pre_process``.
The order indicates the sequence the functions will be executed.
::

  "cs_pre_process": [
    "materialId2Name",
    "calcEmbeddedPoint"
  ],

Then, some execution-related settings are provided.
Use the keywords ``prevabs_cmd_win`` and ``prevabs_cmd_linux`` to set the executable name of preVABS on Windows and Linux, respectively.
::

  "prevabs_cmd_win": "prevabs.exe",
  "prevabs_cmd_linux": "prevabs",

Use the keyword ``solver`` to set the executable name of VABS.
::

  "solver": "VABS",

The keyword ``analysis`` sets what analysis will be carried out by VABS.
In this example, use ``h`` to indicate the cross-sectional analysis (homogenization).
::

  "analysis": "h",

The keyword ``timeout`` is used to prevent the preVABS from stucking in an infinite loop and kill the process when the time is expired.
::

  "timeout": 10,

The keyword ``cross-section_design_template`` sets the cross-section template file name corresponding to a unique cross-section name.
::

  "cross-section_design_template": {
    "uh60a_section": "uh60a_section.xml.tmp"
  },

The keyword ``beam_properties`` indicates the beam properties that will be needed for calculating objective and constraints.
In this example, the properties listed in :numref:`Table %s <tab-props>` will be needed.
::

  "beam_properties": ["mu", "gj", "ei22", "ei33", "sc2", "mc2"],




.. _sect-input-arguments-postpro:

Post-processing
---------------

The last part specifies how to calculate the interim and final outputs.
Since the post-processing functions are mainly scripted by the user, the data structure of this part can be highly flexible and customizable.
In other words, this part of the arguments only provides a place to conveniently make some changes for other similar optimization cases.
User can also put these data in ``data_proc_funcs.py`` completely.

This tutorial only serves as an example.

The keyword is ``post_process`` and all outputs are placed in a list.
Each item in the list specifies one output and how to calculate it.
The inputs for each item are arranged as::

  [output_label, function, arguments, type]

``output_label`` should be the same as those in the Dakota input file if this is a 'final' output.
``function`` can be two types.
If it is ``self``, this means that the value of the ``arguments`` will be directly copied to ``output_label``.
Otherwise, this should be a function defined in the file ``data_proc_funcs.py``.
In this case, ``arguments`` will be passed to the function.
The last entry ``type`` indicates that this output is a final or interim one.

For example, mass per unit length is a constraint and used directly.
This is specified as::

  ["mpl", "self", "mu"]

The difference between the calculated and target torsional stiffnesses is needed to compute the overall difference (``diff``).
The function used is called ``calcRelDiff`` and coded in the file ``data_proc_funcs.py``.
Arguments to this function are the beam property ``gj`` and the target value 24.31e6.
This difference will be stored as an interim output.
Hence, the above setting can be specified as::

  ["gj_diff", "calcRelDiff", ["gj", 24.31e6], "interim"]




Complete file
-------------

.. code-block:: json
    :caption: interface_args.json
    :name: code-arguments

    {

      "scrnout": false,
      "log_level_cmd": "critical",
      "log_level_file": "info",
      "log_file_name": "eval.log",
      
      "prevabs_cmd_win": "prevabs.exe",
      "prevabs_cmd_linux": "prevabs",
      "solver": "VABS",
      "analysis": "h",
      "timeout": 10,


      "cross-section_design_template": {
        "uh60a_section": "uh60a_section.xml.tmp"
      },
      "beam_properties": ["mu", "gj", "ei22", "ei33", "sc2", "mc2"],
      
      
      "data_process_functions_file": "data_proc_funcs",

      "cs_pre_process": [
        "materialId2Name",
        "calcEmbeddedPoint"
      ],

      "post_process": [
        ["mpl", "self", "mu"],
        ["gj_diff", "calcRelDiff", ["gj", 24.31e6], "interim"],
        ["eiflap_diff", "calcRelDiff", ["ei22", 22.2e6], "interim"],
        ["eilag_diff", "calcRelDiff", ["ei33", 835e6], "interim"],
        ["sc2_le_diff", "calcRelDiff", ["sc2", -5.19], "interim"],
        ["mc2_le_diff", "calcRelDiff", ["mc2", -0.822, -5.19], "interim"],
        ["gj", "self", "gj", "interim"],
        ["eif", "self", "ei22", "interim"],
        ["eic", "self", "ei33", "interim"],
        ["sc2", "self", "sc2", "interim"],
        ["mc2", "self", "mc2", "interim"]
      ]

    }

