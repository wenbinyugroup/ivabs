.. include:: /replace.txt

.. _section-ivabs_example_uh60_mopt_stf:

Multiple objective optimization of multiple cross-sections to match target beam properties
===========================================================================================

Problem description
-------------------

The goal and setup are the same as the previous example (:ref:`section-ivabs_example_uh60_sopt_stf`).
The only difference is that this example carries out a multi-objective optimization.



Optimization setup
------------------

Method
~~~~~~

Multi-objective genetic algorithm (MOGA) provided by Dakota is used.
The method is configured in the following way:

* Maximum number of functional evaluations: 20,000
* Size of population: 200
* Random seed: 1027

The rest are default values given by Dakota.



Running of the example
----------------------

1. Go to ``{IVABS_ROOT}\examples\e2_uh60_mopt_stf``.
2. Run ``python run.py uh60_blade.yml``.


Result
------

..  list-table:: Performance of the optimization
    :align: center
    :header-rows: 0

    * - Total number of evaluations
      - 20000
    * - Total running time (wall clock)
      - 22183.4 sec (~= 6 hr 10 min)
    * - CPU model
      - Intel(R) Xeon(R) Gold 6134 CPU @ 3.20GHz
    * - CPU cores
      - 16
    * - Memory
      - 95 GB

..  figure:: /figures/ivabs_ex_uh60_mopt_stf_result_parallel_coord.png
    :name: fig-ivabs_ex_uh60_mopt_stf_result_parallel_coord
    :align: center

    Parallel coordinates plot of the Pareto front.


