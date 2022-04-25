Airfoil Box-spar Uniform
========================


Design concept
--------------

..  figure:: /figures/cs_temp_airfoil_box_uni-components.png
    :name: fig_airfoil_box_uni-components
    :align: center

    Components of the airfoil box-spar design topology.


Some sample designs
~~~~~~~~~~~~~~~~~~~

..  figure:: /figures/cs_temp_airfoil_box_uni-example_1.png
    :name: fig_airfoil_box_uni-example_1
    :width: 6.5in
    :align: center

    Box-spar with two straight spar webs.

..  figure:: /figures/cs_temp_airfoil_box_uni-example_2.png
    :name: fig_airfoil_box_uni-example_2
    :width: 6.5in
    :align: center

    Box-spar with a curved front web and a straight back web.

..  figure:: /figures/cs_temp_airfoil_box_uni-example_3.png
    :name: fig_airfoil_box_uni-example_3
    :width: 6.5in
    :align: center

    Box-spar with two curved spar webs.









Parameters
----------


General parameters
~~~~~~~~~~~~~~~~~~

..  csv-table:: Shape design parameters
    :header: "Name", "Symbol", "Input", "Description"
    :widths: 8, 8, 8, 56

    ``airfoil``,,Required,Airfoil file name (including file extension).
    ``chord``, :math:`c`, Optional (Default=1), Chord length.
    ``gms``, :math:`l^{gm}`, Required, Global mesh size.
    ``fms``, :math:`l^{fm}`, Optional (Default= :math:`10\ l^{gm}`), Filling component mesh size.


Shape parameters
~~~~~~~~~~~~~~~~

All parameters in this section are in the non-dimensional scale (from 0 to 1).

..  figure:: /figures/cs_temp_airfoil_box_uni-shape_params.png
    :name: fig_airfoil_box_uni-shape_params
    :align: center

    Shape parameters.

..  csv-table:: Shape design parameters
    :header: "Name", "Symbol", "Input", "Description"
    :widths: 4, 4, 24, 36

    ``a2p1``,:math:`a_2^{p_1}`,Optional (Default=0.8),Horizontal location of the point :math:`p_1`.
    ``a2p2``,:math:`a_2^{p_2}`,Optional (Default= :math:`a_2^{p_1}`),Horizontal location of the point :math:`p_2`.
    ``a2p3``,:math:`a_2^{p_3}`,Optional (Default=0.6),Horizontal location of the point :math:`p_3`.
    ``a2p4``,:math:`a_2^{p_4}`,Optional (Default= :math:`a_2^{p_3}`),Horizontal location of the point :math:`p_4`.
    ``a2p5``,:math:`a_2^{p_5}`,Optional (Default=0.98),Horizontal location of the point :math:`p_5`.
    ``a2p6``,:math:`a_2^{p_6}`,Optional (Default= :math:`a_2^{p_5}`),Horizontal location of the point :math:`p_6`.
    ``a2p7``,:math:`a_2^{p_7}`,Optional (Default=0.2),Horizontal location of the point :math:`p_7`.
    ``a2p8``,:math:`a_2^{p_8}`,Optional (Default= :math:`a_2^{p_7}`),Horizontal location of the point :math:`p_8`.
    ``a2p9``,:math:`a_2^{p_9}`,Optional (Default=0.1),Horizontal location of the point :math:`p_9`.
    ``a2p10``,:math:`a_2^{p_{10}}`,Optional (Default= :math:`a_2^{p_9}`),Horizontal location of the point :math:`p_{10}`.
    ``a2nsm``,:math:`a_2^{nsm}`,Optional (Default=0.96),Horizontal location of the center of the non-structural mass.
    ``a3nsm``,:math:`a_3^{nsm}`,Optional (Default=0),Vertical location of the center of the non-structural mass.
    ``rnsm``,:math:`r^{nsm}`,Optional (Default=0.005),Radius of the non-structural mass.
    ``kw1``,:math:`k^{w_1}`,Optional (Default=0),Curvature of the front spar web.
    ``kw2``,:math:`k^{w_2}`,Optional (Default=0),Curvature of the back spar web.




Material and layup parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  figure:: /figures/cs_temp_airfoil_box_uni-material_params.png
    :name: fig_airfoil_box_uni-material_params
    :align: center

    Material parameters.


..  csv-table:: Material design parameters
    :header: "Name", "Symbol", "Input", "Description"
    :widths: 8, 8, 8, 56

    ``mi_spar_1``,:math:`l^s`,,Material (lamina) selection of the box spar layup
    ``fo_spar_1``,:math:`\theta_1^s`,,Fiber angle of layer 1 of the box spar layup
    ``fo_spar_2``,:math:`\theta_2^s`,,Fiber angle of layer 2 of the box spar layup
    ``fo_spar_3``,:math:`\theta_3^s`,,Fiber angle of layer 3 of the box spar layup
    ``fo_spar_4``,:math:`\theta_4^s`,,Fiber angle of layer 4 of the box spar layup
    ``np_spar_1``,:math:`n_1^s`,,Number of plies of layer 1 of the box spar layup
    ``np_spar_2``,:math:`n_2^s`,,Number of plies of layer 2 of the box spar layup
    ``np_spar_3``,:math:`n_3^s`,,Number of plies of layer 3 of the box spar layup
    ``np_spar_4``,:math:`n_4^s`,,Number of plies of layer 4 of the box spar layup
    ``mi_le``,:math:`l^c`,,Material (lamina) selection of the cap layup
    ``fo_le``,:math:`\theta^c`,,Fiber angle of the cap layup
    ``np_le``,:math:`n^c`,,Number of plies of the cap layup
    ``mi_te``,:math:`l^o`,,Material (lamina) selection of the overwrap layup
    ``fo_te``,:math:`\theta^o`,,Fiber angle of the overwrap layup
    ``np_te``,:math:`n^o`,,Number of plies of the overwrap layup
