.. include:: replace.txt

.. _example-channel:

Channel
-------

This example has a cross section of a highly heterogeneous channel. This cross section geometry can be defined as shown in :numref:`Fig. %s <fig_channel0>` [CHEN2010]_. The isotropic material properties are given in :numref:`Table %s <table_channel_materials>`. The layup is defined having a single layer with the thickness 0.001524 m. The result is shown in :numref:`Table %s <table_channel_result>` and compared with those in [CHEN2010]_.
Complete input files can be found in ``examples\ex_channel\``, including ``channel.xml``, ``basepoints.dat``, ``baselines.xml``, ``materials.xml``,  and ``layups.xml``.

.. figure:: figures/ex_channel_0.png
  :name: fig_channel0
  :width: 3in

  Cross section of the pipe [CHEN2010]_.

.. figure:: figures/ex_channel_1.png
  :name: fig_channel1
  :width: 6in

  *Base point*\ s, *Base line*\ s and *Segment*\ s of the channel cross section.

.. figure:: figures/ex_channel_mesh.png
  :name: fig_channel_mesh
  :width: 3in

  Meshed cross section viewed in Gmsh.

.. list-table:: Material properties
  :name: table_channel_materials
  :widths: auto
  :header-rows: 2
  :align: center

  * - Name
    - Type
    - Density
    - |e|
    - |nu|
  * - 
    - 
    - |den_si|
    - :math:`10^9` |mod_si|
    - 
  * - mtr1
    - isotropic
    - 1068.69
    - 206.843
    - 0.49

.. list-table:: Layups
  :name: table_channel_layups
  :widths: auto
  :header-rows: 1
  :align: center

  * - Name
    - Layer
    - Material
    - Ply thickness
    - Fiber orientation
    - Number of plies
  * - 
    - 
    - 
    - |len_si|
    - :math:`\circ`
    - 
  * - layup1
    - 1
    - mtr1
    - 0.001524
    - 0
    - 1


.. table:: Results
   :name: table_channel_result

   =================================== ======================== =================================== =================================== =================================== ===================================
   :math:`\phantom{-}1.906\times 10^7` :math:`0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`              :math:`-4.779\times 10^4`           :math:`-1.325\times 10^5`
   :math:`\phantom{-}0.0`              :math:`2.804\times 10^6` :math:`\phantom{-}2.417\times 10^5` :math:`\phantom{-}2.128\times 10^4` :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`
   :math:`\phantom{-}0.0`              :math:`2.417\times 10^5` :math:`\phantom{-}2.146\times 10^6` :math:`-7.663\times 10^3`           :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`
   :math:`\phantom{-}0.0`              :math:`2.128\times 10^4` :math:`-7.663\times 10^3`           :math:`\phantom{-}2.091\times 10^2` :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`
   :math:`-4.779\times 10^4`           :math:`0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}2.011\times 10^3` :math:`\phantom{-}9.104\times 10^2`
   :math:`-1.325\times 10^5`           :math:`0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}9.104\times 10^2` :math:`\phantom{-}1.946\times 10^3`
   =================================== ======================== =================================== =================================== =================================== ===================================

.. table:: Results from reference [CHEN2010]_
   :name: table_channel_result_ref

   =================================== ======================== =================================== =================================== =================================== ===================================
   :math:`\phantom{-}1.903\times 10^7` :math:`0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`              :math:`-4.778\times 10^4`           :math:`-1.325\times 10^5`
   :math:`\phantom{-}0.0`              :math:`2.791\times 10^6` :math:`\phantom{-}2.364\times 10^5` :math:`\phantom{-}2.122\times 10^4` :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`
   :math:`\phantom{-}0.0`              :math:`2.364\times 10^5` :math:`\phantom{-}2.137\times 10^6` :math:`-7.679\times 10^3`           :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`
   :math:`\phantom{-}0.0`              :math:`2.122\times 10^4` :math:`-7.679\times 10^3`           :math:`\phantom{-}2.086\times 10^2` :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`
   :math:`-4.778\times 10^4`           :math:`0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}2.010\times 10^3` :math:`\phantom{-}9.102\times 10^2`
   :math:`-1.325\times 10^5`           :math:`0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}0.0`              :math:`\phantom{-}9.102\times 10^2` :math:`\phantom{-}1.944\times 10^3`
   =================================== ======================== =================================== =================================== =================================== ===================================

