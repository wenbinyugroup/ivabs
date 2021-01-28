.. include:: replace.txt

.. _section-airfoil:

Airfoil
-------

This example demonstrates the capability of building a cross section having an airfoil shape, which is commonly seen on wind turbine blades or helicopter rotor blades. This example is also studied in [CHEN2010]_. A sketch of a cross section for a typical wind turbine blade is shown in :numref:`Fig. %s <fig_mh104_draw>`. The airfoil is MH 104 (http://m-selig.ae.illinois.edu/ads/coord_database.html#M). In this example, the chord length :math:`CL=1.9` m. The origin O is set to the point at 1/4 of the chord. Twist angle :math:`\theta` is :math:`0^\circ`. There are two webs, whose right boundaries are at the 20% and 50% location of the chord, respectively. Both low pressure and high pressure surfaces have four segments. The dividing points between segments are listed in :numref:`Table %s <table_div_pts>`. Materials are given in :numref:`Table %s <table_mh104_materials>` and layups are given in :numref:`Table %s <table_mh104_layups>`. A complete :math:`6\times 6` stiffness matrix is given in :numref:`Table %s <table_airfoil_result>`.
Complete input files can be found in ``examples\ex_airfoil\``, including ``mh104.xml``, ``basepoints.dat``, ``baselines.xml``, ``materials.xml``, and ``layups.xml``.

.. figure:: figures/examplemh1040.png
  :name: fig_mh104_draw
  :width: 5.5in

  Sketch of a cross section for a typical wind turbine blade [CHEN2010]_.

.. list-table:: Dividing points
  :name: table_div_pts
  :widths: auto
  :header-rows: 2
  :align: center

  * - Between segments
    - Low pressure surface
    - High pressure surface
  * - 
    - :math:`(x, y)`
    - :math:`(x, y)`
  * - 1 and 2
    - :math:`(0.004053940, 0.011734800)`
    - :math:`(0.006824530, -0.009881650)`
  * - 2 and 3
    - :math:`(0.114739930, 0.074571970)`
    - :math:`(0.126956710, -0.047620490)`
  * - 3 and 4
    - :math:`(0.536615950, 0.070226120)`
    - :math:`(0.542952100, -0.044437080)`

.. figure:: figures/examplemh1041.png
  :name: fig_mh1041
  :width: 6.5in

  *Base point*\ s of the tube cross section.

.. figure:: figures/examplemh1042.png
  :name: fig_mh1042
  :width: 6.5in

  *Base line*\ s of the tube cross section.

.. figure:: figures/examplemh1043.png
  :name: fig_mh1043
  :width: 6.5in

  *Segment*\ s of the tube cross section.

.. figure:: figures/examplemh104.png
  :name: fig_mh104
  :width: 6.5in

  Meshed cross section viewed in Gmsh.

.. list-table:: Material properties
  :name: table_mh104_materials
  :widths: auto
  :header-rows: 2
  :align: center

  * - Name
    - Type
    - Density
    - |e1|
    - |e2| = |e3|
    - |g12| = |g13| = |g23|
    - |nu12| = |nu13| = |nu23|
  * - 
    - 
    - :math:`10^3` |den_si|
    - :math:`10^9` |mod_si|
    - :math:`10^9` |mod_si|
    - :math:`10^9` |mod_si|
    - 
  * - Uni-directional FRP
    - orthotropic
    - 1.86
    - 37.0
    - 9.00
    - 4.00
    - 0.28
  * - Double-bias FRP
    - orthotropic
    - 1.83
    - 10.3
    - 10.3
    - 8.00
    - 0.30
  * - Gelcoat
    - orthotropic
    - 1.830
    - :math:`\mathrm{10^{-8}}`
    - :math:`\mathrm{10^{-8}}`
    - :math:`\mathrm{10^{-9}}`
    - 0.30
  * - Nexus
    - orthotropic
    - 1.664
    - 10.3
    - 10.3
    - 8.00
    - 0.30
  * - Balsa
    - orthotropic
    - 0.128
    - 0.01
    - 0.01
    - 0.0002
    - 0.30

.. table:: Layups
  :name: table_mh104_layups
  :widths: auto
  :align: center

  +-----------+-------+----------+-----------+----------------+-----------------+
  | Name      | Layer | Material | Ply       | Fiber          | Number          |
  |           |       |          | thickness | orientation    | of plies        |
  +-----------+-------+----------+-----------+----------------+-----------------+
  |           |       |          | |len_si|  | :math:`\circ`  |                 |
  +===========+=======+==========+===========+================+=================+
  | layup_1   | 1     | iso5_3   | 0.000381  | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 2     | iso5_4   | 0.00051   | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 3     | iso5_2   | 0.00053   | 20             | 18              |
  +-----------+-------+----------+-----------+----------------+-----------------+
  | layup_2   | 1     | iso5_3   | 0.000381  | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 2     | iso5_4   | 0.00051   | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 3     | iso5_2   | 0.00053   | 20             | 33              |
  +-----------+-------+----------+-----------+----------------+-----------------+
  | layup_3   | 1     | iso5_3   | 0.000381  | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 2     | iso5_4   | 0.00051   | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 3     | iso5_2   | 0.00053   | 20             | 17              |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 4     | iso5_1   | 0.00053   | 30             | 38              |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 5     | iso5_5   | 0.003125  | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 6     | iso5_1   | 0.00053   | 30             | 37              |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 7     | iso5_2   | 0.00053   | 20             | 16              |
  +-----------+-------+----------+-----------+----------------+-----------------+
  | layup_4   | 1     | iso5_3   | 0.000381  | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 2     | iso5_4   | 0.00051   | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 3     | iso5_2   | 0.00053   | 20             | 17              |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 4     | iso5_5   | 0.003125  | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 5     | iso5_2   | 0.00053   | 0              | 16              |
  +-----------+-------+----------+-----------+----------------+-----------------+
  | layup_web | 1     | iso5_1   | 0.00053   | 0              | 38              |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 2     | iso5_5   | 0.003125  | 0              | 1               |
  |           +-------+----------+-----------+----------------+-----------------+
  |           | 3     | iso5_1   | 0.00053   | 0              | 38              |
  +-----------+-------+----------+-----------+----------------+-----------------+


.. table:: Results
   :name: table_airfoil_result

   =================================== =================================== =================================== =================================== =================================== ===================================
   :math:`\phantom{-}2.411\times 10^9` :math:`\phantom{-}1.567\times 10^6` :math:`\phantom{-}1.125\times 10^7` :math:`-3.279\times 10^7`           :math:`\phantom{-}6.857\times 10^7` :math:`-5.416\times 10^8`
   :math:`\phantom{-}1.567\times 10^7` :math:`\phantom{-}4.435\times 10^8` :math:`-5.759\times 10^6`           :math:`-2.018\times 10^7`           :math:`\phantom{-}1.600\times 10^7` :math:`-1.093\times 10^6`
   :math:`\phantom{-}1.125\times 10^7` :math:`-5.759\times 10^6`           :math:`\phantom{-}2.701\times 10^7` :math:`-8.087\times 10^5`           :math:`\phantom{-}1.612\times 10^5` :math:`-6.104\times 10^6`
   :math:`-3.279\times 10^7`           :math:`-2.018\times 10^7`           :math:`-8.087\times 10^5`           :math:`\phantom{-}2.156\times 10^7` :math:`-2.099\times 10^6`           :math:`\phantom{-}8.969\times 10^5`
   :math:`\phantom{-}6.857\times 10^7` :math:`\phantom{-}1.600\times 10^7` :math:`\phantom{-}1.612\times 10^5` :math:`-2.099\times 10^6`           :math:`\phantom{-}2.153\times 10^7` :math:`-9.465\times 10^6`
   :math:`-5.416\times 10^8`           :math:`-1.093\times 10^6`           :math:`-6.104\times 10^6`           :math:`\phantom{-}8.969\times 10^5` :math:`-9.465\times 10^6`           :math:`\phantom{-}4.772\times 10^8`
   =================================== =================================== =================================== =================================== =================================== ===================================

.. table:: Results from reference [CHEN2010]_
   :name: table_airfoil_result_ref

   =================================== =================================== =================================== =================================== =================================== ===================================
   :math:`\phantom{-}2.389\times 10^9` :math:`\phantom{-}1.524\times 10^6` :math:`\phantom{-}6.734\times 10^6` :math:`-3.382\times 10^7`           :math:`-2.627\times 10^7`           :math:`-4.736\times 10^8`
   :math:`\phantom{-}1.524\times 10^6` :math:`\phantom{-}4.334\times 10^8` :math:`-3.741\times 10^6`           :math:`-2.935\times 10^5`           :math:`\phantom{-}1.527\times 10^7` :math:`\phantom{-}3.835\times 10^5`
   :math:`\phantom{-}6.734\times 10^6` :math:`-3.741\times 10^6`           :math:`\phantom{-}2.743\times 10^7` :math:`-4.592\times 10^4`           :math:`-6.869\times 10^2`           :math:`-4.742\times 10^6`
   :math:`-3.382\times 10^7`           :math:`-2.935\times 10^5`           :math:`-4.592\times 10^4`           :math:`\phantom{-}2.167\times 10^7` :math:`-6.279\times 10^4`           :math:`\phantom{-}1.430\times 10^6`
   :math:`-2.627\times 10^7`           :math:`\phantom{-}1.527\times 10^7` :math:`-6.869\times 10^2`           :math:`-6.279\times 10^4`           :math:`\phantom{-}1.970\times 10^7` :math:`\phantom{-}1.209\times 10^7`
   :math:`-4.736\times 10^8`           :math:`\phantom{-}3.835\times 10^5` :math:`-4.742\times 10^6`           :math:`\phantom{-}1.430\times 10^6` :math:`\phantom{-}1.209\times 10^7` :math:`\phantom{-}4.406\times 10^8`
   =================================== =================================== =================================== =================================== =================================== ===================================

.. note:: The errors between the result and the reference are caused by the difference of modeling of the trailing edge. If reduce the trailing edge skin to a single thin layer, then the difference between the trailing edge shapes is minimized, and the two resulting stiffness matrices are basically the same, as shown in :numref:`Fig. %s <fig_mh104_comparison>`.

.. figure:: figures/examplemh104_comparison.png
  :name: fig_mh104_comparison
  :width: 6in

  Comparison of stiffness matrices after modifying the trailing edge.

