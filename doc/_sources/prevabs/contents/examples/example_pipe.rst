.. _example-pipe:

Pipe
====

Probelm description
-------------------

.. figure:: /figures/examplepipe0.png
  :name: fig_pipe_draw
  :width: 6in
  :align: center

  Cross section of the pipe [YU2005]_.

This example has the cross section as shown in :numref:`Fig. %s <fig_pipe_draw>` [YU2005]_.
This cross section has two straight walls and two half circular walls.
:math:`r=1.0` in. and other dimensions are shown in the figure.
Each wall has the layup having two layers made from one material.
Fiber orientations for each layer are also given in the figure.
Material properties and layups are given in :numref:`Table %s <table_pipe_materials>` and :numref:`Table %s <table_pipe_layups>`.
Cross-sectional properties are given in :numref:`Table %s <table_pipe_result>` and compared with the results from [YU2005]_.
The tiny differences are due to different meshes.
Complete input files can be found in ``examples\ex_pipe\``, including ``pipe.xml``, ``baselines.xml``, ``materials.xml``, and ``layups.xml``.

.. figure:: /figures/examplepipe1.png
  :name: fig_pipe1
  :width: 6in
  :align: center

  *Base point*\ s and *Base line*\ s of the pipe cross section.

.. figure:: /figures/examplepipe2.png
  :name: fig_pipe2
  :width: 6in
  :align: center

  *Segment*\ s of the pipe cross section.

.. figure:: /figures/examplepipe.png
  :name: fig_pipe
  :width: 6in
  :align: center

  Meshed cross section viewed in Gmsh.

.. csv-table:: Material properties
  :name: table_pipe_materials
  :header-rows: 2
  :align: center

  "Name", "Density", |e1|, |e2|, |e3|, |g12|, |g13|, |g23|, |nu12|, |nu13|, |nu23|
   , |den_im|, |mod_im_m|, |mod_im_m|, |mod_im_m|, |mod_im_m|, |mod_im_m|, |mod_im_m|, , ,
  "mat_1", 0.057, 20.59, 1.42, 1.42, 0.87, 0.87, 0.87, 0.42, 0.42, 0.42

.. csv-table:: Layups
  :name: table_pipe_layups
  :header-rows: 2
  :align: center

  "Name", "Layer", "Material", "Ply thickness", "Orientation", "Number of plies"
  , , , |len_im|, :math:`\circ`,
  "layup_1", 1, "mat_1", 0.1, 0, 1
  ,          2, "mat_1", 0.1, 90, 1
  "layup_2", 1, "mat_1", 0.1, -45, 1
  ,          2, "mat_1", 0.1, 45, 1




Result
------

.. table:: Results
   :name: table_pipe_result
   :align: center

   ========================== ====================================== ======================================
   Component                  Value                                  Reference [YU2005]_
   ========================== ====================================== ======================================
   :math:`S_{11}` [|stf0_im|] :math:`\phantom{-}1.03892 \times 10^7` :math:`\phantom{-}1.03890 \times 10^7`
   :math:`S_{22}` [|stf0_im|] :math:`\phantom{-}7.85800 \times 10^5` :math:`\phantom{-}7.84299 \times 10^5`
   :math:`S_{33}` [|stf0_im|] :math:`\phantom{-}3.31330 \times 10^5` :math:`\phantom{-}3.29002 \times 10^5`
   :math:`S_{14}` [|stf1_im|] :math:`\phantom{-}9.74568 \times 10^4` :math:`\phantom{-}9.82878 \times 10^4`
   :math:`S_{25}` [|stf1_im|] :math:`-8.02785 \times 10^3`           :math:`-8.18782 \times 10^3`
   :math:`S_{36}` [|stf1_im|] :math:`-5.14533 \times 10^4`           :math:`-5.18541 \times 10^4`
   :math:`S_{44}` [|stf2_im|] :math:`\phantom{-}6.89600 \times 10^5` :math:`\phantom{-}6.86973 \times 10^5`
   :math:`S_{55}` [|stf2_im|] :math:`\phantom{-}1.88230 \times 10^6` :math:`\phantom{-}1.88236 \times 10^6`
   :math:`S_{66}` [|stf2_im|] :math:`\phantom{-}5.38985 \times 10^6` :math:`\phantom{-}5.38972 \times 10^6`
   ========================== ====================================== ======================================

