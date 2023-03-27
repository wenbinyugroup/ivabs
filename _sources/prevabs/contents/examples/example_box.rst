.. _example-box-beam:

Box beam
========

Problem description
-------------------

.. figure:: /figures/examplebox0.png
  :name: fig_box_draw
  :width: 4in
  :align: center

  Cross section of the box beam [YU2012]_.

This example is a thin-walled box beam whose cross section is depicted in :numref:`Fig. %s <fig_box_draw>` [YU2012]_.
The width :math:`a_2=0.953` in, height :math:`a_3=0.530` in, and thickness :math:`t=0.030` in.
Each wall has six plies of the same composite material and the same fiber orientation of :math:`15^\circ`.
Material properties and layup scheme are listed in :numref:`Table %s <table_box_materials>` and :numref:`Table %s <table_box_layups>`.
Cross-sectional properties are given in :numref:`Table %s <table_box_result>` and compared with those in Ref. [YU2012]_.
The tiny differences are due to different meshes.
Complete input files can be found in ``examples\ex_box\``, including ``box.xml`` and ``materials.xml``.

.. figure:: /figures/examplebox1.png
  :name: fig_box1
  :width: 6in
  :align: center

  *Base point*\ s, *Base line*\ s and *Segment*\ s of the box beam cross section.

.. figure:: /figures/examplebox.png
  :name: fig_box
  :width: 6in
  :align: center

  Meshed cross section viewed in Gmsh.

.. tabularcolumns:: |l|l|r|r|r|r|r|r|r|r|r|r|

.. csv-table:: Material properties
  :name: table_box_materials
  :header-rows: 2
  :align: center

  "Name", "Density", |e1|, |e2|, |e3|, |g12|, |g13|, |g23|, |nu12|, |nu13|, |nu23|
   , |den_im|, |mod_im_m|, |mod_im_m|, |mod_im_m|, |mod_im_m|, |mod_im_m|, |mod_im_m|, , ,
  "mat_1", 0.0001353, 20.59, 1.42, 1.42, 0.87, 0.87, 0.696, 0.30, 0.30, 0.34

.. csv-table:: Layups
  :name: table_box_layups
  :header-rows: 2
  :align: center

  "Name", "Layer", "Material", "Ply thickness", "Orientation", "Number of plies"
  , , , |len_im|, :math:`\circ`,
  "layup1", 1, "mat_1", 0.05, -15, 6





Result
------

.. table:: Results
   :name: table_box_result
   :align: center

   ========================== ==================================== ====================================
   Component                  Value                                Reference [YU2012]_
   ========================== ==================================== ====================================
   :math:`S_{11}` [|stf0_im|] :math:`\phantom{-}1.437 \times 10^6` :math:`\phantom{-}1.437 \times 10^6`
   :math:`S_{22}` [|stf0_im|] :math:`\phantom{-}9.026 \times 10^4` :math:`\phantom{-}9.027 \times 10^4`
   :math:`S_{33}` [|stf0_im|] :math:`\phantom{-}3.941 \times 10^4` :math:`\phantom{-}3.943 \times 10^4`
   :math:`S_{14}` [|stf1_im|] :math:`\phantom{-}1.074 \times 10^5` :math:`\phantom{-}1.074 \times 10^5`
   :math:`S_{25}` [|stf1_im|] :math:`-5.201 \times 10^4`           :math:`-5.201 \times 10^4`
   :math:`S_{36}` [|stf1_im|] :math:`-5.635 \times 10^4`           :math:`-5.635 \times 10^4`
   :math:`S_{44}` [|stf2_im|] :math:`\phantom{-}1.679 \times 10^4` :math:`\phantom{-}1.679 \times 10^4`
   :math:`S_{55}` [|stf2_im|] :math:`\phantom{-}6.621 \times 10^4` :math:`\phantom{-}6.621 \times 10^4`
   :math:`S_{66}` [|stf2_im|] :math:`\phantom{-}1.725 \times 10^5` :math:`\phantom{-}1.725 \times 10^5`
   ========================== ==================================== ====================================

