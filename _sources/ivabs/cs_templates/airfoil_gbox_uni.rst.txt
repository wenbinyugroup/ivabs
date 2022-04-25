Airfoil Box-spar Uniform
========================


Design concept
--------------

..  figure:: /figures/cs_temp_airfoil_gbox_uni-components.png
    :name: fig_airfoil_box_uni-components
    :align: center

    Components of the airfoil box-spar design topology.


Some sample designs
~~~~~~~~~~~~~~~~~~~

..  figure:: /figures/cs_temp_airfoil_gbox_uni-example_1.png
    :name: fig_airfoil_box_uni-example_1
    :width: 6.5in
    :align: center

    Box-spar with two straight spar webs.

..  figure:: /figures/cs_temp_airfoil_gbox_uni-example_2.png
    :name: fig_airfoil_box_uni-example_2
    :width: 6.5in
    :align: center

    Box-spar with a curved front web and a straight back web.









Parameters
----------

*Italics value* in the "Input" column is the default.

General parameters
~~~~~~~~~~~~~~~~~~

..  csv-table:: General design parameters
    :header: "Name", "Type", "Input", "Symbol", "Description"
    :widths: 4, 4, 20, 4, 48

    airfoil, String, Required, , Airfoil file name (including file extension).
    chord, Float, Optional (*1*), :math:`c`, Chord length.
    gms, Float, Required, :math:`l^{gm}`, Global mesh size.
    fms, Float, Optional (*10\*gms*), :math:`l^{fm}`, Filling component mesh size.
    mdb_name, String, Required, , Material database file name.
    elm_type, String, "Optional (choose one from: *linear*, quadratic)", , Element type.

Shape parameters
~~~~~~~~~~~~~~~~

All parameters in this section are in the non-dimensional scale (from 0 to 1).

..  figure:: /figures/cs_temp_airfoil_gbox_uni-shape_params.png
    :name: fig_airfoil_box_uni-shape_params
    :align: center

    Shape parameters.

..  csv-table:: Shape design parameters
    :header: "Name", "Type", "Input", "Symbol", "Description"
    :widths: 4, 4, 20, 4, 48

    a2p1, Float, Optional (*0.8*), :math:`a_2^{p_1}`, Horizontal location of the point :math:`p_1`.
    a2p2, Float, Optional (*a2p2*), :math:`a_2^{p_2}`, Horizontal location of the point :math:`p_2`.
    a2p3, Float, Optional (*0.6*), :math:`a_2^{p_3}`, Horizontal location of the point :math:`p_3`.
    a2p4, Float, Optional (*a2p3*), :math:`a_2^{p_4}`, Horizontal location of the point :math:`p_4`.
    a2p5, Float, Optional (*0.98*), :math:`a_2^{p_5}`, Horizontal location of the point :math:`p_5`.
    a2p6, Float, Optional (*a2p5*), :math:`a_2^{p_6}`, Horizontal location of the point :math:`p_6`.
    a2p7, Float, Optional (*0.2*), :math:`a_2^{p_7}`, Horizontal location of the point :math:`p_7`.
    a2p8, Float, Optional (*a2p7*), :math:`a_2^{p_8}`, Horizontal location of the point :math:`p_8`.
    a2p9, Float, Optional (*0.1*), :math:`a_2^{p_9}`, Horizontal location of the point :math:`p_9`.
    a2p10, Float, Optional (*a2p9*), :math:`a_2^{p_{10}}`,Horizontal location of the point :math:`p_{10}`.
    a2nsm, Float, Optional (*0.96*), :math:`a_2^{nsm}`, Horizontal location of the center of the non-structural mass.
    a3nsm, Float, Optional (*0*), :math:`a_3^{nsm}`, Vertical location of the center of the non-structural mass.
    rnsm, Float, Optional (*0.005*), :math:`r^{nsm}`, Radius of the non-structural mass.
    kw1, Float, Optional (*0*), :math:`k^{w_1}`, Curvature of the front spar web.
    kw2, Float, Optional (*0*), :math:`k^{w_2}`, Curvature of the back spar web.




Material and layup parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  figure:: /figures/cs_temp_airfoil_gbox_uni-material_params.png
    :name: fig_airfoil_box_uni-material_params
    :align: center

    Material parameters.


..  csv-table:: Material design parameters
    :header: "Name", "Type", "Input", "Symbol", "Description"
    :widths: 4, 4, 20, 4, 48

    lam_spar_1,     String,  Required,                :math:`l_1^m`,      Lamina selection of layer 1 of the box spar layup
    lam_spar_2,     String,  Optional (*lam_spar_1*), :math:`l_2^m`,      Lamina selection of layer 2 of the box spar layup
    lam_spar_3,     String,  Optional (*lam_spar_1*), :math:`l_3^m`,      Lamina selection of layer 3 of the box spar layup
    lam_spar_4,     String,  Optional (*lam_spar_1*), :math:`l_4^m`,      Lamina selection of layer 4 of the box spar layup
    ang_spar_1,     Float,   Optional (*0*),          :math:`\theta_1^m`, Fiber angle of layer 1 of the box spar layup
    ang_spar_2,     Float,   Optional (*0*),          :math:`\theta_2^m`, Fiber angle of layer 2 of the box spar layup
    ang_spar_3,     Float,   Optional (*0*),          :math:`\theta_3^m`, Fiber angle of layer 3 of the box spar layup
    ang_spar_4,     Float,   Optional (*0*),          :math:`\theta_4^m`, Fiber angle of layer 4 of the box spar layup
    ply_spar_1,     Integer, Optional (*1*),          :math:`n_1^m`,      Number of plies of layer 1 of the box spar layup
    ply_spar_2,     Integer, Optional (*1*),          :math:`n_2^m`,      Number of plies of layer 2 of the box spar layup
    ply_spar_3,     Integer, Optional (*1*),          :math:`n_3^m`,      Number of plies of layer 3 of the box spar layup
    ply_spar_4,     Integer, Optional (*1*),          :math:`n_4^m`,      Number of plies of layer 4 of the box spar layup
    lam_skin,       String,  Required,                :math:`l^s`,        Lamina selection of the skin layer
    ang_skin,       Float,   Optional (*0*),          :math:`\theta^s`,   Fiber angle of the skin layer
    ply_skin,       Integer, Optional (*1*),          :math:`n^s`,        Number of plies of the skin layer
    lam_cap,        String,  Required,                :math:`l^c`,        Lamina selection of the cap layer
    ang_cap,        Float,   Optional (*0*),          :math:`\theta^c`,   Fiber angle of the cap layer
    ply_cap,        Integer, Optional (*1*),          :math:`n^c`,        Number of plies of the cap layer
    lam_front,      String,  Required,                :math:`l^f`,        Lamina selection of the front layup
    ang_front,      Float,   Optional (*0*),          :math:`\theta^f`,   Fiber angle of the front layup
    ply_front,      Integer, Optional (*1*),          :math:`n^f`,        Number of plies of the front layup
    lam_back,       String,  Required,                :math:`l^b`,        Lamina selection of the back layup
    ang_back,       Float,   Optional (*0*),          :math:`\theta^b`,   Fiber angle of the back layup
    ply_back,       Integer, Optional (*1*),          :math:`n^b`,        Number of plies of the back layup
    mat_nsm,        String,  Required,                :math:`m^{nsm}`,    Material selection of the non-structural mass
    mat_fill_front, String,  Required,                :math:`m^{ff}`,     Material selection of the front filling
    mat_fill_back,  String,  Required,                :math:`m^{bf}`,     Material selection of the back filling
    mat_fill_te,    String,  Required,                :math:`m^{tf}`,     Material selection of the trailing filling









Full template
-------------


..  literalinclude:: airfoil_gbox_uni.xml.tmp
    :language: xml
    :linenos:

