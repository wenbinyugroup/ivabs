.. _section-ivabs_example_uh60_sopt_stf:

Single objective optimization of multiple cross-sections to match target beam properties
===========================================================================================

Problem description
-------------------

The goal of this problem is to design a composite rotor blade for some desired beam properties, which could be given from an old design or requirements from rotor simulations.

The target beam properties are listed in the table below.

..  csv-table:: Target beam properties
    :header: :math:`r/R`, :math:`GJ`, :math:`EI_f`, :math:`EI_c`
    :widths: 10, 10, 10, 10
    :header-rows: 1

    , |stf1_im_ft|, |stf1_im_ft|, |stf1_im_ft|
    0.2, 0.17976e6, 0.19162e6, 0.32572e7
    0.3, 0.16882e6, 0.15417e6, 0.59786e7
    0.4, 0.16882e6, 0.15417e6, 0.57986e7
    0.5, 0.17058e6, 0.16042e6, 0.58384e7
    0.6, 0.17208e6, 0.16042e6, 0.58396e7
    0.7, 0.17208e6, 0.16319e6, 0.48434e7
    0.8, 0.13337e6, 0.12709e6, 0.37748e7
    0.9, 0.47441e6, 0.38724e6, 0.91526e7
    0.9371, 0.66027e6, 0.53895e6, 0.12738e8
    1, 22757, 6927.3, 0.41657e6




Parameterization
----------------

As illustrated in the previous section, parameters should be identified first at the two levels.
At the cross-sectional level, consider a box-spar type structure as the design concept or topology, as shown in :numref:`Fig. %s <fig-ivabs_ex_uh60_sopt_stf_cs_geo_params>` and :numref:`Fig. %s <fig-ivabs_ex_uh60_sopt_stf_cs_mat_params>`.
:numref:`Fig. %s <fig-ivabs_ex_uh60_sopt_stf_cs_geo_params>` shows the parameters controlling the shape and size of components, such as locations of spar webs, and location and size of the non-structural mass.
:numref:`Fig. %s <fig-ivabs_ex_uh60_sopt_stf_cs_mat_params>` shows the parameters controlling the layup scheme of box spar, front and back laminates, including material selection, fiber angle, and number of plies.


..  figure:: /figures/cs_temp_airfoil_gbox_uni-shape_params.png
    :name: fig-ivabs_ex_uh60_sopt_stf_cs_geo_params
    :align: center

    Shape parameters.

..  figure:: /figures/cs_temp_airfoil_gbox_uni-material_params.png
    :name: fig-ivabs_ex_uh60_sopt_stf_cs_mat_params
    :align: center

    Material parameters.


At the blade level, distribution functions of cross-sectional parameters are defined.
In this study, three types of distributions are considered: constant, linear interpolation, and step interpolation.
A summary of cross-sectional parameters and corresponding distribution functions are given in :numref:`Table %s <tab-ivabs_ex_uh60_sopt_stf_params>`.

..  list-table:: Summary of blade level distributions of cross-sectional parameters.
    :name: tab-ivabs_ex_uh60_sopt_stf_params
    :align: center
    :header-rows: 1

    * - Cross-sectional parameter
      - Blade level distribution
      - Description
    * - :math:`a^{wl}_2`
      - Linear interpolation of six pairs of :math:`(\bar{r}, \bar{a}^{wl}_2)`
      - Location of the front (leading) spar web
    * - :math:`a^{wt}_2`
      - Linear interpolation of six pairs of :math:`(\bar{r}, \bar{a}^{wt}_2)`
      - Location of the back (trailing) spar web
    * - :math:`a^{nsm}_2`
      - Linear interpolation of six pairs of :math:`(\bar{r}, \bar{a}^{nsm}_2)`
      - Location of the non-structural mass center
    * - :math:`r^{nsm}`
      - Constant function :math:`\bar{r}^{nsm}`
      - Radius of the non-structural mass
    * - :math:`\theta^s_1,\theta^s_2,\theta^s_3,\theta^s_4`
      - Step interpolation of five pairs of :math:`(\bar{r}, \bar{\theta}^s_i)`
      - Fiber angle of layer :math:`i` of the box spar layup
    * - :math:`n^s`
      - Step interpolation of five pairs of :math:`(\bar{r}, \bar{n}^s_i)`
      - Number of plies of each layer of the box spar layup
    * - :math:`\theta^f,\theta^b`
      - Constant function of :math:`\bar{\theta}^f` and :math:`\bar{\theta}^b`
      - Fiber angle of each layer of the front and back layups
    * - :math:`n^f,n^b`
      - Constant function of :math:`\bar{n}^f` and :math:`\bar{n}^b`
      - Number of plies of each layer of the front and back layups
    * - :math:`l^s, l^f, l^b`
      - Constant function of :math:`\bar{l}^s`, :math:`\bar{l}^f` and :math:`\bar{l}^b`
      - Lamina choice of each layer of the box spar, front, and back layups

More details on the parameterization can be found in the section :ref:`section-ivabs_parameterization`.





Optimization setup
------------------

Design variables
~~~~~~~~~~~~~~~~

The coefficients controlling the distribution functions listed in :numref:`Table %s <tab-ivabs_ex_uh60_sopt_stf_params>` are the true design variables in the optimization.
A summary of design variables is given in :numref:`Table %s <tab-ivabs_ex_uh60_sopt_stf_design_variables>`.


..  list-table:: Design variables
    :name: tab-ivabs_ex_uh60_sopt_stf_design_variables
    :align: center
    :header-rows: 1

    * - Design variable
      - Symbol in optimization
      - Type
      - Range
      - Description
    * - :math:`(\bar{a}^{wl}_2)_1,\dots,(\bar{a}^{wl}_2)_6`
      - :math:`x_1,\dots,x_6`
      - Continuous
      - [0.8, 0.9]
      - Coefficients of the interpolation function for the leading spar web location :math:`a^{wl}_2` (non-dimensional)
    * - :math:`(\bar{a}^{wt}_2)_1,\dots,(\bar{a}^{wt}_2)_6`
      - :math:`x_{7},\dots,x_{12}`
      - Continuous
      - [0.5, 0.7]
      - Coefficients of the interpolation function for the trailing spar web location :math:`a^{wt}_2` (non-dimensional)
    * - :math:`(\bar{a}^{nsm}_2)_1,\dots,(\bar{a}^{nsm}_2)_6`
      - :math:`x_{13},\dots,x_{18}`
      - Continuous
      - [0.95, 0.985]
      - Coefficients of the interpolation function for the non-structural mass center location :math:`a^{nsm}_2` (non-dimensional)
    * - :math:`\bar{r}^{nsm}`
      - :math:`x_{19}`
      - Continuous
      - [0.001, 0.01]
      - Radius of the non-structural mass for the whole blade (non-dimensional)
    * - :math:`(\bar{\theta}^{s}_1)_1,\dots,(\bar{\theta}^{s}_1)_5`
      - :math:`x_{20},\dots,x_{24}`
      - Discrete
      - [-89, 90]
      - Coefficients of the interpolation function for fiber angle of layer 1 of the spar layup :math:`\theta^{s}_1`
    * - :math:`(\bar{\theta}^{s}_2)_1,\dots,(\bar{\theta}^{s}_2)_5`
      - :math:`x_{25},\dots,x_{29}`
      - Discrete
      - [-89, 90]
      - Coefficients of the interpolation function for fiber angle of layer 2 of the spar layup :math:`\theta^{s}_2`
    * - :math:`(\bar{\theta}^{s}_3)_1,\dots,(\bar{\theta}^{s}_3)_5`
      - :math:`x_{30},\dots,x_{34}`
      - Discrete
      - [-89, 90]
      - Coefficients of the interpolation function for fiber angle of layer 3 of the spar layup :math:`\theta^{s}_3`
    * - :math:`(\bar{\theta}^{s}_4)_1,\dots,(\bar{\theta}^{s}_4)_5`
      - :math:`x_{35},\dots,x_{39}`
      - Discrete
      - [-89, 90]
      - Coefficients of the interpolation function for fiber angle of layer 4 of the spar layup :math:`\theta^{s}_4`
    * - :math:`(\bar{n}^{s})_1,\dots,(\bar{n}^{s})_5`
      - :math:`x_{40},\dots,x_{44}`
      - Discrete
      - [1, 20]
      - Coefficients of the interpolation function for number of plies of the spar layup :math:`n^{s}`
    * - :math:`\bar{\theta}^{f}`
      - :math:`x_{45}`
      - Discrete
      - [-89, 90]
      - Fiber angle of the front (leading) layup :math:`\theta^{f}`
    * - :math:`\bar{\theta}^{b}`
      - :math:`x_{46}`
      - Discrete
      - [-89, 90]
      - Fiber angle of the back (trailing) layup :math:`\theta^{b}`
    * - :math:`\bar{n}^{f}`
      - :math:`x_{47}`
      - Discrete
      - [1, 20]
      - Number of plies of the front (leading) layup :math:`n^{f}`
    * - :math:`\bar{n}^{b}`
      - :math:`x_{48}`
      - Discrete
      - [1, 20]
      - Number of plies of the back (trailing) layup :math:`n^{b}`
    * - :math:`\bar{l}^{s}`
      - :math:`x_{49}`
      - Discrete
      - [1, 4]
      - Lamina choice of the spar layup :math:`l^{s}`
    * - :math:`\bar{l}^{f}`
      - :math:`x_{50}`
      - Discrete
      - [1, 4]
      - Lamina choice of the front (leading) layup :math:`l^{f}`
    * - :math:`\bar{l}^{b}`
      - :math:`x_{51}`
      - Discrete
      - [1, 4]
      - Lamina choice of the back (trailing) layup :math:`l^{b}`




Objective function
~~~~~~~~~~~~~~~~~~

To match the target beam properties, this example uses the weighted sum method, i.e., to minimize the maximum absolute value among the three differences of the calculated properties from the targets:

..  math::
    :label: eq_ivabs_ex_opt_obj

    f(\mathbf{x}) = w_1 \left| \frac{GJ-\hat{GJ}}{\hat{GJ}} \right| + w_2 \left| \frac{EI_f-\hat{EI}_f}{\hat{EI}_f} \right| + w_3 \left| \frac{EI_c-\hat{EI}_c}{\hat{EI}_c} \right|

where :math:`\hat{(\cdot)}` is the target value.


Constraints
~~~~~~~~~~~

No other constraints are considered in this example beside the boundary constraints of design variables.

Method
~~~~~~

Single objective genetic algorithm (SOGA) provided by Dakota is used.
The method is configured in the following way:

* Maximum number of functional evaluations: 20,000
* Size of population: 200
* Random seed: 1027
* Evaluation concurrency: 20

The rest are default values given by Dakota.



Running of the example
----------------------

1. Go to ``{IVABS_ROOT}\examples\e1_uh60_sopt_stf``.
2. Run ``python run.py uh60_blade.yml``.


Result
------

..  list-table:: Performance of the optimization
    :align: center
    :header-rows: 0

    * - Total number of evaluations
      - 16873
    * - Total running time (wall clock)
      - 20568.8 sec (~= 5 hr 40 min)
    * - CPU model
      - Intel(R) Xeon(R) Gold 6134 CPU @ 3.20GHz
    * - CPU cores
      - 16
    * - Memory
      - 95 GB


Evolution
~~~~~~~~~

..  figure:: /figures/ivabs_ex_uh60_sopt_stf_result_obj_histr.png
    :name: fig-ivabs_ex_uh60_sopt_stf_result_obj_histr
    :align: center

    Evoluation of the objective function.



Final design
~~~~~~~~~~~~

..  figure:: /figures/ivabs_ex_uh60_sopt_stf_result_prop_compare.png
    :name: fig-ivabs_ex_uh60_sopt_stf_result_prop_compare
    :align: center

    Comparison of beam properties between the optimum design and target values.

..  figure:: /figures/ivabs_ex_uh60_sopt_stf_result_blade_plot.png
    :name: fig-ivabs_ex_uh60_sopt_stf_result_blade_plot
    :align: center

    Plot of the ten cross-sections of the optimum design.

.. Total number of functional evaluations and running time can be found at the end of the file ``cs_tm_opt_soga_{PLATFORM}.out``.

.. Evolution results can be found in files ``population_i.dat``, where ``i`` is the generation number.

.. Final design result can be found in the file ``finaldata1.dat``, which contains design variables, responses (objective and constraints) of the optimum desgin.

.. Evoluation
.. ~~~~~~~~~~

.. The optimization process stops when reaching the convergence condition.
.. The total number of functional evaluation is 15,060.

.. Final design
.. ~~~~~~~~~~~~

.. .. list-table:: Final design
..    :align: center
..    :header-rows: 1

..    * - Symbol
..      - Value
..      - Unit
..    * - :math:`a_2^{wl}`
..      - :math:`-0.137`
..      - 1
..    * - :math:`a_2^{wt}`
..      - :math:`-0.364`
..      - 1
..    * - :math:`\theta_1`
..      - :math:`-43`
..      - degree
..    * - :math:`\theta_2`
..      - :math:`0`
..      - degree
..    * - :math:`\theta_3`
..      - :math:`74`
..      - degree
..    * - :math:`\theta_4`
..      - :math:`70`
..      - degree



.. .. list-table:: Comparison of final and target beam properties
..    :align: center
..    :header-rows: 1

..    * - 
..      - :math:`EA` [|stf0_im|]
..      - :math:`GJ` [|stf1_im|]
..      - :math:`EI_f` [|stf1_im|]
..      - :math:`EI_l` [|stf1_im|]
..      - :math:`SC_2` [|len_im|]
..      - :math:`MC_2` [|len_im|]
..    * - Target
..      - :math:`52.25 \times 10^6`
..      - :math:`24.20 \times 10^6`
..      - :math:`25.00 \times 10^6`
..      - :math:`1.058 \times 10^9`
..      - :math:`-5.253`
..      - :math:`-5.972`
..    * - Optimized
..      - :math:`52.16 \times 10^6`
..      - :math:`24.22 \times 10^6`
..      - :math:`24.95 \times 10^6`
..      - :math:`1.061 \times 10^9`
..      - :math:`-5.267`
..      - :math:`-5.960`
..    * - Difference [%]
..      - :math:`0.172`
..      - :math:`0.074`
..      - :math:`-0.185`
..      - :math:`0.268`
..      - :math:`0.258`
..      - :math:`-0.201`
