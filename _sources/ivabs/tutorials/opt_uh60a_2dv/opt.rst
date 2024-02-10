
.. _opt:

Optimization Formulation
========================


Design variables
----------------

Two parameters controlling the size and location of the box spar will be treated as design variables in this example.

.. list-table:: Design variables
    :align: center
    :header-rows: 1

    * - Name in input files
      - Design range
      - Variable type
      - Description
    * - ``wl_a2``
      - [-0.2, -0.1]
      - Continuous
      - Non-dimensional horizontal location of the leading web from the leading edge
    * - ``wt_a2``
      - [-0.5, -0.3]
      - Continuous
      - Non-dimensional horizontal location of the leading web from the leading edge




Fixed parameters
----------------

All other cross-sectional parameters are fixed and summarized in :numref:`Table %s <tab-param-fixed>`

.. list-table:: Fixed parameters
    :name: tab-param-fixed
    :align: center
    :header-rows: 1

    * - Name in input files
      - Value
      - Type
      - Description
    * - ``chord``
      - 20.76
      - Real
      - Chord length of the cross-section
    * - ``pfte2_a2``
      - -0.9
      - Real
      - Non-dimensional location of point marking the coarse meshes in the filling region
    * - ``mesh_size``
      - 0.04
      - Real
      - Global mesh size
    * - ``mesh_size_fill``
      - 0.3
      - Real
      - Mesh size for the filling regions
    * - ``oa2``
      - -0.25
      - Real
      - Non-dimensional horizontal location of the model center (quarter chord)
    * - ``pnsmc_a2``
      - -0.046
      - Real
      - Non-dimensional horizontal coordinate of the center of the non-structural mass
    * - ``pnsmc_a3``
      - 0.0
      - Real
      - Non-dimensional vertical coordinate of the center of the non-structural mass
    * - ``nsmr``
      - 0.0094
      - Real
      - Non-dimensional radius of the non-structural mass
    * - ``mi_spar_1``
      - 4
      - Integer
      - Material (lamina) selection of the box spar layup
    * - ``fo_spar_1``
      - 50
      - Integer
      - Fiber angle of layer 1 of the box spar layup
    * - ``fo_spar_2``
      - -9
      - Integer
      - Fiber angle of layer 2 of the box spar layup
    * - ``fo_spar_3``
      - 53
      - Integer
      - Fiber angle of layer 3 of the box spar layup
    * - ``fo_spar_4``
      - -44
      - Integer
      - Fiber angle of layer 4 of the box spar layup
    * - ``np_spar_1``
      - 16
      - Integer
      - Number of plies of layer 1 of the box spar layup
    * - ``np_spar_2``
      - 16
      - Integer
      - Number of plies of layer 2 of the box spar layup
    * - ``np_spar_3``
      - 14
      - Integer
      - Number of plies of layer 3 of the box spar layup
    * - ``np_spar_4``
      - 19
      - Integer
      - Number of plies of layer 4 of the box spar layup
    * - ``mi_le``
      - 1
      - Integer
      - Material (lamina) selection of the cap layup
    * - ``fo_le``
      - -36
      - Integer
      - Fiber angle of the cap layup
    * - ``np_le``
      - 16
      - Integer
      - Number of plies of the cap layup
    * - ``mi_te``
      - 4
      - Integer
      - Material (lamina) selection of the overwrap layup
    * - ``fo_te``
      - 71
      - Integer
      - Fiber angle of the overwrap layup
    * - ``np_te``
      - 13
      - Integer
      - Number of plies of the overwrap layup
    


Objective
---------

To minimize the difference between the calculated beam properties and target ones.
The min-max method is used in this example.
The difference is measured as the maximum one among the differences (absolute values) of all beam properties considered.

.. math::

  f = \max \{ |d_i|,\quad i = 1 \text{ to } 5 \},

where

.. math::

    \begin{aligned}
      d_1 &= \frac{GJ - \hat{GJ}}{\hat{GJ}} \\
      d_2 &= \frac{EI_f - \hat{EI}_f}{\hat{EI}_f} \\
      d_3 &= \frac{EI_l - \hat{EI}_l}{\hat{EI}_l} \\
      d_4 &= \frac{SC_2^{le} - \hat{SC}_2^{le}}{\hat{SC}_2^{le}} \\
      d_5 &= \frac{MC_2^{le} - \hat{MC}_2^{le}}{\hat{MC}_2^{le}}
    \end{aligned}




Method
------

Genetic algorithm will be used in this example.

The population size is set to 50.

The stopping conditions are two-fold:

#. Convergence: Check if the change of average fitness among the last 10 generations is less than 10%
#. Maximum functional evaluations: 2000

