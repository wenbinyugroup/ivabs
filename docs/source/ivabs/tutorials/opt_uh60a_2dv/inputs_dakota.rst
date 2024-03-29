
.. _sect-input-dakota:

Dakota Input File (``cs_tm_opt_soga.dakota``)
=============================================

Dakota inputs are grouped into five sections: environment, method, model, variables, interface and responses.
The general rule is to use keywords followed by values.
The alignment of keywords and values are not important.
They can share the same line or use multiple lines.
Indentations are not required and used in this example only for clarity and showing the hierarchical relation of keywords.
The equal sign ``=`` is also optional.
Comments are specified by the character ``#``.

For more details on the input syntax and keywords, please check the Dakota user manual and reference manual.









.. _dakota-input-environment:

Environment
-----------

This section starts with the keyword ``environment``.
This section configurs some general settings such as the names of various output files.

The keyword ``output_file`` specifies the main output of the optimization.
This file is given the name ``cs_tm_opt_soga.out``::

  output_file = 'cs_tm_opt_soga.out'

The keyword ``write_restart`` specifies the file that is used to restart the optimization if it stops at some point for some reason.
This file is given the name ``cs_tm_opt_soga.rst``::

  write_restart = 'cs_tm_opt_soga.rst'

The keyword ``error_file`` specifies the file that stores the error messages if Dakota stops with some exceptions.
This file is given the name ``cs_tm_opt_soga.err``::

  error_file = 'cs_tm_opt_soga.err'

The keyword ``tabular_data`` specifies a file that writes tabular results of variable and response history.
This file is given the name ``cs_tm_opt_soga_tabular.dat``::

  tabular_data
    tabular_data_file = 'cs_tm_opt_soga_tabular.dat'









.. _dakota-input-method:

Method
------

This section is specified by the keyword ``method`` and configures the optimization method.
As stated earlier, this example will use Genetic Algorithm.
For this single objective optimization problem, the specific method is SOGA (Single Objective Genetic Algorithm) and the corresponding keyword is ``soga``::

  method
    soga

The number of individual designs in a single generation is specified by the keyword ``population_size``, which is set to 50::

  population_size = 50

The stopping condition of the optimization contains two aspects.
One is the convergence checking and the other is the maximum number of functional evaluations.
The settings are::

  max_function_evaluations = 2000
  convergence_type
    average_fitness_tracker
      percent_change = 0.1
      num_generations = 10

To control the randomness in the algorithm, a randomness seed is specified using the keyword ``seed``::

  seed = 1027

The following two settings can be used to provide more information of the optimization process.
The keyword ``print_each_pop`` ask Dakota to write tabular data (variables and responses) into a file after each generation.
The output file will be ``population_i.dat``, where ``i`` is the generation number.
The keyword ``log_file`` specifies the name for the file storing logging messages generated by SOGA.
The inputs are::

  print_each_pop
  log_file = 'cs_tm_opt_soga.log'

For other settings that are not mentioned here, readers can go to the Dakota reference manual for their detailed usage and default values.









.. _dakota-input-model:

Model
-----

The ``model`` section configures how variables are mapped into responses.
This example uses the default and simplest model: ``single``, where variables are mapped to responses through the process specified in ``interface``.
::

    model
      single









.. _dakota-input-variables:

Variables
---------

This section specifies variables in this optimization problem, using the keyword ``variables``.
Following the terminology of Dakota, variables in this example can be grouped into two types, design variables and state variables.
Design variables are those that will be changed in each iteration, while state variables are those that will be fixed in an optimization study.

As stated in Section: :ref:`opt`, there are two continuous design variables in this example.
The corresponding inputs are::

  continuous_design = 2
    descriptors     =  'wl_x2'  'wt_x2'
    upper_bounds    =   -0.10    -0.30
    lower_bounds    =   -0.20    -0.50

All other parameters mentioned in Section: :ref:`sect-cs-param` are treated as state variables.
The keyword ``discrete_state_set`` is used to specify their fixed values.
There are eight real-type state variables::

  real = 8
    descriptors = 'mesh_size'  'mesh_size_fill'
                  'pnsmc_x3'        'pfte2_x2'
                  'pnsmc_x2'            'nsmr'
                      'chord'             'oa2'
    elements    =       0.04               0.3
                          0              -0.9
                      -0.046            0.0094
                      20.76             -0.25

There are 15 integer-type state variables::

  integer = 15
    descriptors  = 'mi_spar_1'  'mi_le'  'mi_te'
                  'np_spar_1'  'np_le'  'np_te'
                  'np_spar_2'
                  'np_spar_3'
                  'np_spar_4'
                  'fo_spar_1'  'fo_le'  'fo_te'
                  'fo_spar_2'
                  'fo_spar_3'
                  'fo_spar_4'
    elements = 4 1 4
              16 16 13
              16
              14
              19
              50 -36 71
              -9
              53
              -44









.. _dakota-input-interface:

Interface
---------

This section specifies how Dakota should run and change data with the analysis.
The keyword is ``interface``.
The command used to call the analysis is specified by the keyword ``analysis_driver``.
Since the analysis is coded in a Python script and data (inputs/outputs) are transferred through files, the ``fork`` type is used for this analysis driver::

  analysis_driver = 'python3 interface.py interface_args.json uh60a_section'
    fork

The names of the parameters file (written by Dakota) and the results file (read by Dakota) are specified as::

  parameters_file = 'input.in'
  results_file = 'output.out'

Hence, the actual shell command called by Dakota will be

.. code-block:: shell

  python3 interface.py interface_args.json uh60a_section input.in output.out

All files generated by the analysis can be saved by using the keyword ``file_save``.
If the storage is limited, then all files can be deleted after each successful evaluation by commenting out this keyword.

To use the concurrent computing technique provided by Dakota, each individual analysis must be carried out in an isolated working directory.
In this example, each analysis is done in a folder named ``evals/eval_i``, where ``i`` is the ``directory_tag``, which is also the evaluation number.
Same as ``file_save``, ``directory_save`` is also optional.
This is specified as::

  work_directory
    named = 'evals/eval'
    directory_tag
    directory_save

To make the analysis driver work, the final step is to specify all files needed by the analysis driver, using the keyword ``link_file`` (Linux) or ``copy_file`` (Windows)::

  link_file = 'interface.py'
              'interface_args.json'
              'data_proc_funcs.py'
              'design/*'

In this example, the following six files are needed:

#. ``design/uh60a_section.xml.tmp`` (see Section: :ref:`sect-input-template`)
#. ``design/material_database.xml`` (see Section: :ref:`sect-input-material`)
#. ``design/sc1095.dat`` (see Section: :ref:`sect-input-airfoil`)
#. ``interface.py`` (see Section: :ref:`sect-input-interface`)
#. ``interface_args.json`` (see Section: :ref:`sect-input-arguments`)
#. ``data_proc_funcs.py`` (see Section: :ref:`sect-input-process`)

Finally, this example runs 20 concurrent analyses each time.
This is specified as::

  asynchronous
    evaluation_concurrency = 20









.. _dakota-input-responses:

Responses
---------

This section specifies the responses sent pack to Dakota from the analysis driver, including objectives and constraints.
Based on the optimization formulation in Section: :ref:`opt`, Dakota will read two responses from the result file, one objective and one constraint::

  responses
    descriptors = 'diff' 'mpl'

The objective is to minimize the difference between the calculated and target beam properties::

  objective_functions = 1
    sense = 'min'

The constraint is keep the calculated mass less than the target value::

  nonlinear_inequality_constraints = 1
    upper_bounds =  0.00149
    lower_bounds =        0

Since the optimization method is Genetic Algorithm, there is no gradient and hessian results returned to Dakota.









Complete file
-------------

.. code-block:: none
    :caption: cs_tm_opt_soga.dakota
    :name: code-dakota

    # ====================================================================

    environment
      output_file = 'cs_tm_opt_soga.out'
      write_restart = 'cs_tm_opt_soga.rst'
      error_file = 'cs_tm_opt_soga.err'
      tabular_data
        tabular_data_file = 'cs_tm_opt_soga_tabular.dat'

    # ====================================================================

    method
      soga
        max_function_evaluations = 2000
        population_size = 50
        seed = 1027
        convergence_type
          average_fitness_tracker  # default
            percent_change = 0.1  # defualt: 0.1
            num_generations = 10  # default: 10
        print_each_pop
        log_file = 'cs_tm_opt_soga.log'

    # ====================================================================

    model
      single

    # ====================================================================

    variables
      active design

      continuous_design = 2
        descriptors     =  'wl_x2'  'wt_x2'
        upper_bounds    =   -0.10    -0.30
        lower_bounds    =   -0.20    -0.50

      discrete_state_set
        real = 8
          descriptors = 'mesh_size'  'mesh_size_fill'
                        'pnsmc_x3'        'pfte2_x2'
                        'pnsmc_x2'            'nsmr'
                            'chord'             'oa2'
          elements    =       0.04               0.3
                                0              -0.9
                            -0.046            0.0094
                            20.76             -0.25
        integer = 15
          descriptors  = 'mi_spar_1'  'mi_le'  'mi_te'
                        'np_spar_1'  'np_le'  'np_te'
                        'np_spar_2'
                        'np_spar_3'
                        'np_spar_4'
                        'fo_spar_1'  'fo_le'  'fo_te'
                        'fo_spar_2'
                        'fo_spar_3'
                        'fo_spar_4'
          elements = 4 1 4
                    16 16 13
                    16
                    14
                    19
                    50 -36 71
                    -9
                    53
                    -44


    # ====================================================================

    interface
      analysis_driver = 'python3 interface.py interface_args.json'
        fork
          parameters_file = 'input.in'
          results_file = 'output.out'
          file_save
          work_directory
            named = 'evals/eval'
            directory_tag
            directory_save
            link_file = 'interface.py'
                        'interface_args.json'
                        'data_proc_funcs.py'
                        'design/*'
      asynchronous
        evaluation_concurrency = 20

    # ====================================================================

    responses
      descriptors = 'diff' 'mpl'
      objective_functions = 1
        sense = 'min'
        nonlinear_inequality_constraints = 1
          upper_bounds =  0.00149
          lower_bounds =        0
      no_gradients
      no_hessians

