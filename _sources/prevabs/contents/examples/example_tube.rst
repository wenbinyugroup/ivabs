.. _example-tube:

Circular tube
=============

Problem description
-------------------


This example has a cross section of a simple circular shape with radius :math:`r=10` m.
This cross section geometry can be defined easily by a center and a radius.
Material properties are given in :numref:`Table %s <table_tube_materials>`.
The layup is defined using the stacking sequence code :math:`[\pm 45_2/0_2/90]_{2s}`.
The result is given in :numref:`Table %s <table_tube_result>`.
Complete input files can be found in ``examples\ex_tube\``, including
``tube.xml`` and ``materials.xml``.

.. figure:: /figures/examplecircle1.png
  :name: fig_circle1
  :width: 6in
  :align: center

  *Base point*\ s, *Base line*\ s and *Segment*\ s of the tube cross section.

.. figure:: /figures/examplecircle.png
  :name: fig_circle
  :width: 4in
  :align: center

  Meshed cross section viewed in Gmsh.

.. csv-table:: Material properties
  :name: table_tube_materials
  :header-rows: 2
  :align: center

  "Name", "Type", "Density", |e1|, |e2|, |e3|, |g12|, |g13|, |g23|, |nu12|, |nu13|, |nu23|
   , , |den_si_k|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, , ,
  "iso5_4", "orthotropic", 1.664, 10.3, 10.3, 10.3, 8.0, 8.0, 8.0, 0.3, 0.3, 0.3

.. csv-table:: Layups
  :name: table_tube_layups
  :header-rows: 1
  :align: center

  "Name", "Material", "Stacking sequence"
  "layup1", "iso5_4", :math:`[\pm 45_2/0_2/90]_{s}`





Result
------

.. table:: Results
   :name: table_tube_result

   ======================================= ======================================= ======================================= ====================================== ======================================= =======================================
   :math:`\phantom{-}1.108\times 10^{12}`  :math:`-2.677\times 10^{-3}`            :math:`-1.050\times 10^{-4}`            :math:`-5.795\times 10^{-5}`           :math:`-2.099\times 10^5`               :math:`-1.626\times 10^5`
   :math:`-2.677\times 10^{-3}`            :math:`\phantom{-}2.352\times 10^{11}`  :math:`-1.583\times 10^3`               :math:`\phantom{-}4.781\times 10^4`    :math:`\phantom{-}3.200\times 10^{-3}`  :math:`\phantom{-}2.063\times 10^{-2}` 
   :math:`-1.050\times 10^{-4}`            :math:`-1.583\times 10^3`               :math:`\phantom{-}2.352\times 10^{11}`  :math:`\phantom{-}4.086\times 10^4`    :math:`\phantom{-}6.546\times 10^{-4}`  :math:`\phantom{-}1.063\times 10^{-3}`
   :math:`-5.795\times 10^{-5}`            :math:`\phantom{-}4.781\times 10^4`     :math:`\phantom{-}4.086\times 10^4`     :math:`\phantom{-}4.043\times 10^{13}` :math:`\phantom{-}2.717\times 10^{-7}`  :math:`\phantom{-}3.229\times 10^{-8}`
   :math:`-2.099\times 10^5`               :math:`\phantom{-}3.200\times 10^{-3}`  :math:`\phantom{-}6.546\times 10^{-4}`  :math:`\phantom{-}2.717\times 10^{-7}` :math:`\phantom{-}4.819\times 10^{13}`  :math:`-1.399\times 10^6`
   :math:`-1.626\times 10^5`               :math:`\phantom{-}2.063\times 10^{-2}`  :math:`\phantom{-}1.063\times 10^{-3}`  :math:`\phantom{-}3.229\times 10^{-8}` :math:`-1.399\times 10^6`               :math:`\phantom{-}4.819\times 10^{13}`
   ======================================= ======================================= ======================================= ====================================== ======================================= =======================================

