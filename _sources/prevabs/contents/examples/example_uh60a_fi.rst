.. _section-uh60a-fi:

UH-60A (Initial Failure Analysis)
=================================

Run the example
---------------

::

  prevabs -i uh60a.xml -fi -e -v


Problem description
-------------------

.. Two load cases are used to show the visualization of safe and failed structures.

.. csv-table:: Load case
  :name: table_uh60a_loadcases
  :header-rows: 1
  :align: center

  ":math:`F_1` [lb]", ":math:`F_2` [lb]", ":math:`F_3` [lb]", ":math:`M_1` [lb.in]", ":math:`M_2` [lb.in]", ":math:`M_3` [lb.in]"
  46777, 250.762, 414.939, -306.1, -16131.9, 2727.67





Result
------

With this load case, the structure fails.
The minimum strength ratio is 0.814.
The element that has this value is 18252.

.. For both cases, the minimum strength ratio will always be the lower bound of the colormap range.
.. The difference is the upper bound.
.. Any value greater than the upper bound will be shown in the same color as the upper bound.

.. - For the safe and critical load cases (strength ratio >= 1), the upper bound is ten times the lower bound.
.. - For the failed load case (strength ratio < 1), the upper bound is "2 - lower bound". In other words, the critical strength ratio (1) will always be at the middle.

.. .. figure:: /figures/ex-uh60a_fi_safe.png
..   :name: fig_uh60a_fi_safe
..   :width: 6in
..   :align: center

..   Contour plot of strength ratio for the safe load case.

.. figure:: /figures/ex-uh60a_fi_fail_2.png
  :name: fig_uh60a_fi_fail
  :width: 6in
  :align: center

  Contour plot of strength ratio.

.. figure:: /figures/ex-uh60a_fi_fail_2_zoomin.png
  :name: fig_uh60a_fi_fail_zoomin
  :width: 6in
  :align: center

  Contour plot of strength ratio (zoom in).


