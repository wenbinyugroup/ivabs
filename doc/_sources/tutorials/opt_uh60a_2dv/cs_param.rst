
.. _sect-cs-param:

Cross-sectional Parameterization and Beam Properties
====================================================


The cross-section is comprised of the following components: box spar, front laminate, back laminate, front filling, back filling and non-structural mass, as shown in :numref:`Fig. %s <fig-cs_comp>`.

.. figure:: figures/cs_comp.png
    :name: fig-cs_comp
    :align: center

    Components of the cross-section.




Parameterization
----------------

Parameters can be in general grouped into two sets, geometry related and layup related.

Geometry
^^^^^^^^

In this example, four geometric parameters are defined in the non-dimensional frame where the chord length is 1, as shown in :numref:`Fig. %s <fig-cs_param_geo>`.
The origin of this frame is placed at the leading edge.
The size and location of the box spar are defined by the two parameters :math:`a_2^{wl}` and :math:`a_2^{wt}`, which are in fact the horizontal coordinates of the leading and trailing webs, respectively.
The non-structural mass is assumed to be a circular object in this example.
Hence, the three parameters defining the size and location are the horizontal coordinate :math:`a_2^{nsm}` and vertical coordinate :math:`a_3^{nsm}` of the center, and the radius :math:`r^{nsm}`.

.. figure:: figures/cs_param_geo.png
    :name: fig-cs_param_geo
    :align: center

    Parameters for the geometry in the non-dimensional frame, where the chord length is 1.

Layup
^^^^^

Layup related parameters are used to define materials (:math:`l`), fiber angles (:math:`\theta`) and numbers of plies (:math:`n`) for the laminates of box spar, cap and overwrap.
In this example, the box spar laminate is assumed to have four layers.
All four layers have the same material (:math:`l^s`), but can have different fiber angles (:math:`\theta_1^s, \theta_2^s, \theta_3^s, \theta_4^s`) and numbers of plies (:math:`n_1^s, n_2^s, n_3^s, n_4^s`).
The cap laminate is assumed to have a single layer with three parameters: :math:`l^c, \theta^c, n^c`.
The overwrap laminate is also assumed having a single layer with three parameters: :math:`l^o, \theta^o, n^o`.

The overall layup design of the three lamiante components are listed in :numref:`Table %s <tab-layup-box>`, :numref:`Table %s <tab-layup-front>` and :numref:`Table %s <tab-layup-back>`.

.. list-table:: Layup of the box spar laminate
    :name: tab-layup-box
    :align: center
    :header-rows: 1

    * - Layer
      - Lamina
      - Fiber angle [deg]
      - Ply count
    * - Base
      - T300 15k/976
      - 0
      - 2
    * - 1
      - :math:`l^s`
      - :math:`\theta^s_1`
      - :math:`n^s_1`
    * - 2
      - :math:`l^s`
      - :math:`\theta^s_2`
      - :math:`n^s_2`
    * - 3
      - :math:`l^s`
      - :math:`\theta^s_3`
      - :math:`n^s_3`
    * - 4
      - :math:`l^s`
      - :math:`\theta^s_4`
      - :math:`n^s_4`

.. list-table:: Layup of the front laminate
    :name: tab-layup-front
    :align: center
    :header-rows: 1

    * - Layer
      - Lamina
      - Fiber angle [deg]
      - Ply count
    * - Cap
      - Aluminum 8009
      - 0
      - 2
    * - Base
      - T300 15k/976
      - 0
      - 2
    * - 1
      - :math:`l^f`
      - :math:`\theta^f`
      - :math:`n^f`

.. list-table:: Layup of the back laminate
    :name: tab-layup-back
    :align: center
    :header-rows: 1

    * - Layer
      - Lamina
      - Fiber angle [deg]
      - Ply count
    * - Base
      - T300 15k/976
      - 0
      - 2
    * - 1
      - :math:`l^b`
      - :math:`\theta^b`
      - :math:`n^b`

.. .. figure:: figures/cs_param_layup.png
..     :name: fig-cs_param_layup
..     :align: center

..     Layups for the three components: cap, box and overwrap.


A summary of the parameters is listed in :numref:`Table %s <tab-params>`.

.. list-table:: Summary of parameters
    :name: tab-params
    :align: center
    :header-rows: 1

    * - Symbol
      - Name in input files
      - Description
    * - :math:`a_2^{wl}`
      - ``wl_a2``
      - Non-dimensional horizontal coordinate of the leading web of the box spar
    * - :math:`a_2^{wt}`
      - ``wt_a2``
      - Non-dimensional horizontal coordinate of the trailing web of the box spar
    * - :math:`a_2^{nsm}`
      - ``pnsmc_a2``
      - Non-dimensional horizontal coordinate of the center of the non-structural mass
    * - :math:`a_3^{nsm}`
      - ``pnsmc_a3``
      - Non-dimensional vertical coordinate of the center of the non-structural mass
    * - :math:`r^{nsm}`
      - ``nsmr``
      - Non-dimensional radius of the non-structural mass
    * - :math:`l^s`
      - ``mi_spar_1``
      - Material (lamina) selection of the box spar layup
    * - :math:`\theta_1^s`
      - ``fo_spar_1``
      - Fiber angle of layer 1 of the box spar layup
    * - :math:`\theta_2^s`
      - ``fo_spar_2``
      - Fiber angle of layer 2 of the box spar layup
    * - :math:`\theta_3^s`
      - ``fo_spar_3``
      - Fiber angle of layer 3 of the box spar layup
    * - :math:`\theta_4^s`
      - ``fo_spar_4``
      - Fiber angle of layer 4 of the box spar layup
    * - :math:`n_1^s`
      - ``np_spar_1``
      - Number of plies of layer 1 of the box spar layup
    * - :math:`n_2^s`
      - ``np_spar_2``
      - Number of plies of layer 2 of the box spar layup
    * - :math:`n_3^s`
      - ``np_spar_3``
      - Number of plies of layer 3 of the box spar layup
    * - :math:`n_4^s`
      - ``np_spar_4``
      - Number of plies of layer 4 of the box spar layup
    * - :math:`l^c`
      - ``mi_le``
      - Material (lamina) selection of the cap layup
    * - :math:`\theta^c`
      - ``fo_le``
      - Fiber angle of the cap layup
    * - :math:`n^c`
      - ``np_le``
      - Number of plies of the cap layup
    * - :math:`l^o`
      - ``mi_te``
      - Material (lamina) selection of the overwrap layup
    * - :math:`\theta^o`
      - ``fo_te``
      - Fiber angle of the overwrap layup
    * - :math:`n^o`
      - ``np_te``
      - Number of plies of the overwrap layup

Some other parameters used are listed below:

.. list-table:: Summary of other parameters
    :name: tab-params-others
    :align: center
    :header-rows: 1

    * - Name in input files
      - Description
    * - ``chord``
      - Chord length of the cross-section
    * - ``oa2``
      - Non-dimensional horizontal coordinate of the origin of the frame :math:`\mathbf{x}` used in VABS.
    * - ``pfte2_a2``
      - Non-dimensional location of point marking the coarse meshes in the filling region
    * - ``mesh_size``
      - Global mesh size
    * - ``mesh_size_fill``
      - Mesh size for the filling regions




Materials
---------

Materials used in this example are summarized in :numref:`Table %s <tab-materials>`.
Lamina thickness is given in :numref:`Table %s <tab-thickness>`.
'Aluminum 80009' is used as the outermost layer of the cap.
'Lead' is used for the non-structural mass.
'Rohacell 70' is used at the leading filling region.
'Plascore PN2-3/16OX3.0' is used at the trailing filling region.
'T300 15k/976' is used as the base layer for the spar, cap and overwrap, to prevent zero layers during the optimization.
The last four rows in the table are the candidate materials for the layup design of the three components.

.. list-table:: Material properties
    :name: tab-materials
    :align: center
    :header-rows: 1

    * - Material
      - Density
      - :math:`E_1`
      - :math:`E_2`
      - :math:`E_3`
      - :math:`\nu_{12}`
      - :math:`\nu_{13}`
      - :math:`\nu_{23}`
      - :math:`G_{12}`
      - :math:`G_{13}`
      - :math:`G_{23}`
    * - 
      - [:math:`\mathrm{lbf\cdot s^2/in^4}`]
      - [:math:`\mathrm{psi}`]
      - [:math:`\mathrm{psi}`]
      - [:math:`\mathrm{psi}`]
      - 
      - 
      - 
      - [:math:`\mathrm{psi}`]
      - [:math:`\mathrm{psi}`]
      - [:math:`\mathrm{psi}`]
    * - Aluminum 8009
      - :math:`0.271959\times 10^{-3}`
      - :math:`13.1\times 10^6`
      -
      -
      - :math:`0.33`
      -
      -
      -
      -
      -
    * - Lead
      - :math:`1.060957\times 10^{-3}`
      - :math:`1.0\times 10^{-3}`
      -
      -
      - :math:`0`
      -
      -
      -
      -
      -
    * - Rohacell 70
      - :math:`7.040895\times 10^{-6}`
      - :math:`13.125\times 10^3`
      - :math:`13.125\times 10^3`
      - :math:`13.125\times 10^3`
      - :math:`0.315`
      - :math:`0.315`
      - :math:`0.300`
      - :math:`4.118\times 10^3`
      - :math:`4.118\times 10^3`
      - :math:`4.118\times 10^3`
    * - Plascore PN2-3/16OX3.0
      - :math:`4.509066\times 10^{-6}`
      - :math:`1.0\times 10^3`
      - :math:`1.0\times 10^3`
      - :math:`20\times 10^3`
      - :math:`0.30`
      - :math:`0.01`
      - :math:`0.01`
      - :math:`1.0\times 10^3`
      - :math:`3.5\times 10^3`
      - :math:`5.799\times 10^3`
    * - T300 15k/976
      - :math:`0.149716\times 10^{-3}`
      - :math:`19.6\times 10^6`
      - :math:`1.34\times 10^6`
      -
      - :math:`0.348`
      -
      -
      - :math:`0.91\times 10^6`
      -
      -
    * - AS4 12k/E7K8
      - :math:`0.145973\times 10^{-3}`
      - :math:`19.3\times 10^6`
      - :math:`1.23\times 10^6`
      -
      - :math:`0.32`
      -
      -
      - :math:`7.31\times 10^6`
      -
      -
    * - S2/SP381
      - :math:`0.173109\times 10^{-3}`
      - :math:`7.05\times 10^6`
      - :math:`1.97\times 10^6`
      -
      - :math:`0.263`
      -
      -
      - :math:`0.59\times 10^6`
      -
      -
    * - T650-35 12k/976
      - :math:`0.148781\times 10^{-3}`
      - :math:`22.0\times 10^6`
      - :math:`1.30\times 10^6`
      -
      - :math:`0.115`
      -
      -
      - :math:`0.745\times 10^6`
      -
      -
    * - T700 24K/E765
      - :math:`0.145037\times 10^{-3}`
      - :math:`18.71\times 10^6`
      - :math:`1.36\times 10^6`
      -
      - :math:`0.319`
      -
      -
      - :math:`0.65\times 10^6`
      -
      -


.. list-table:: Lamina thickness
    :name: tab-thickness
    :align: center
    :header-rows: 1

    * - Material
      - Thickness [:math:`in`]
    * - Aluminum 8009
      - 0.01
    * - T300 15k/976
      - 0.0053
    * - AS4 12k/E7K8
      - 0.0054
    * - S2/SP381
      - 0.0092
    * - T650-35 12k/976
      - 0.0052
    * - T700 24K/E765
      - 0.0056




Properties
----------

The beam properties calculated by VABS listed in :numref:`Table %s <tab-props>` will be needed in the optimization.
:numref:`Fig. %s <fig-cs_props>` shows the points and axes with respect to which some properties are calculated.
The two bending stiffnesses are given with respect to the principal bending axes.
The horizontal locations of the shear and mass centers are given with respect to the modeling origin, which is the quarder chord in this example.

.. figure:: figures/cs_prop.png
    :name: fig-cs_props
    :align: center

    Beam properties and their reference of calculation.



A summary of the properties is listed in :numref:`Table %s <tab-props>`.

.. list-table:: Summary of properties
    :name: tab-props
    :align: center
    :header-rows: 1

    * - Symbol
      - Name in input files
      - Description
    * - :math:`m`
      - ``mu``
      - Mass per unit length
    * - :math:`GJ`
      - ``gj``
      - Torsional stiffness
    * - :math:`EI_f`
      - ``ei22``
      - Flapping bending stiffness
    * - :math:`EI_l`
      - ``ei33``
      - Lead-lag bending stiffness
    * - :math:`SC_2`
      - ``sc2``
      - Horizontal coordinate of the shear center in the frame x.
    * - :math:`MC_2`
      - ``mc2``
      - Horizontal coordinate of the mass center in the frame x.
