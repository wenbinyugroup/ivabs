.. _example-i-beam:

I-beam
------

.. figure:: /figures/exampleibeam0.png
  :name: fig_ibeam_draw
  :width: 6in
  :align: center

  Meshed cross section viewed in Gmsh.

This example has an I-shape cross section. The dimensions shown in
:numref:`Fig. %s <fig_ibeam_draw>` are :math:`w_1=2.0` m, :math:`w_2=3.0` m,
:math:`h=3.0` m, :math:`t_1=0.11` m, :math:`t_2=0.065` m, :math:`t_w=0.08` m.
Materials and layups are given in :numref:`Table %s <table_ibeam_materials>`
and :numref:`Table %s <table_ibeam_layups>`. The effective stiffness
matrix is listed in :numref:`Table %s <table_ibeam_result>`.
Complete input files can be found in ``examples\ex_ibeam\``, including
``ibeam.xml``, ``basepoints.dat``, ``baselines.xml``, ``materials.xml``,
and ``layups.xml``.

.. figure:: /figures/exampleibeam1.png
  :name: fig_ibeam1
  :width: 6in
  :align: center

  *Base point*\ s, *Base line*\ s and *Segment*\ s of the I beam cross section.

.. figure:: /figures/exampleibeam.png
  :name: fig_ibeam
  :width: 4in
  :align: center

  Meshed cross section viewed in Gmsh.

.. csv-table:: Material properties
  :name: table_ibeam_materials
  :header-rows: 2
  :align: center

  "Name", "Type", "Density", |e1|, |e2|, |e3|, |g12|, |g13|, |g23|, |nu12|, |nu13|, |nu23|
   , , |den_si_k|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, , ,
  "iso5_1", "orthotropic", 1.86, 37.00, 9.00, 9.00, 4.00, 4.00, 4.00, 0.28, 0.28, 0.28
  "iso5_2", "orthotropic", 1.83, 10.30, 10.30, 10.30, 8.00, 8.00, 8.00, 0.30, 0.30, 0.30
  "iso5_3", "orthotropic", 1.83, 1e-8, 1e-8, 1e-8, 1e-9, 1e-9, 1e-9, 0.30, 0.30, 0.30
  "iso5_4", "orthotropic", 1.664, 10.30, 10.30, 10.30, 8.00, 8.00, 8.00, 0.30, 0.30, 0.30
  "iso5_5", "orthotropic", 0.128, 0.01, 0.01, 0.01, 2e-4, 2e-4, 2e-4, 0.30, 0.30, 0.30

.. csv-table:: Layups
  :name: table_ibeam_layups
  :header-rows: 2
  :align: center

  "Name", "Layer", "Material", "Ply thickness", "Orientation", "Number of plies"
  , , , |len_si|, :math:`\circ`,
  "layup1", 1, "iso5_1", 0.03, 90, 2
  ,         2, "iso5_2", 0.05, 0, 1
  "layup2", 1, "iso5_3", 0.015, 0, 3
  ,         2, "iso5_4", 0.02, 90, 1
  "layup_web", 1, "iso5_5", 0.02, 0, 4


.. table:: Results
   :name: table_ibeam_result

   =================================== ====================================== ======================================= ======================================= ======================================= =======================================
   :math:`\phantom{-}2.749\times 10^9` :math:`-4.763\times 10^{-8}`           :math:`-1.505\times 10^{-14}`           :math:`-5.734\times 10^{-8}`            :math:`-1.945\times 10^9`               :math:`\phantom{-}2.779\times 10^3`
   :math:`-4.763\times 10^{-8}`        :math:`\phantom{-}1.362\times 10^9`    :math:`\phantom{-}4.309\times 10^2`     :math:`\phantom{-}1.645\times 10^9`     :math:`\phantom{-}1.277\times 10^{-7}`  :math:`-4.362\times 10^{-14}`
   :math:`-1.505\times 10^{-14}`       :math:`\phantom{-}4.309\times 10^2`    :math:`\phantom{-}4.729\times 10^4`     :math:`\phantom{-}5.201\times 10^2`     :math:`\phantom{-}4.038\times 10^{-14}` :math:`-4.775\times 10^{-13}`
   :math:`-5.734\times 10^{-8}`        :math:`\phantom{-}1.645\times 10^9`    :math:`\phantom{-}5.201\times 10^2`     :math:`\phantom{-}1.990\times 10^9`     :math:`\phantom{-}1.541\times 10^{-7}`  :math:`\phantom{-}7.025\times 10^{-14}`
   :math:`-1.945\times 10^9`           :math:`\phantom{-}1.277\times 10^{-7}` :math:`\phantom{-}4.038\times 10^{-14}` :math:`\phantom{-}1.541\times 10^{-7}`  :math:`\phantom{-}5.376\times 10^9`     :math:`-5.274\times 10^2`
   :math:`\phantom{-}2.779\times 10^3` :math:`-4.362\times 10^{-14}`          :math:`-4.775\times 10^{-13}`           :math:`\phantom{-}7.025\times 10^{-14}` :math:`-5.274\times 10^2`               :math:`\phantom{-}1.173\times 10^9`
   =================================== ====================================== ======================================= ======================================= ======================================= =======================================
