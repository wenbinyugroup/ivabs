.. _tutorial:

Tutorial
========

This tutorial provides a walkthrough for how to prepare input files for
PreVABS given a cross section design.

The design of a cross section
-----------------------------

.. figure:: /figures/tutorial_box_0.png
  :name: fig_tutorial_box
  :width: 6in
  :align: center

  A box-beam cross section.

The box-beam cross section shown in :numref:`Fig. %s <fig_tutorial_box>`
will be used in this tutorial. All four walls and two webs are made from
composite laminates. The two webs are symmetric about a middle vertical
line. They are inclined such that the upper portion of both webs are
closer to each other than the lower portion. The central space enclosed
by the top and bottom walls and two webs is filled with an isotropic
material.

The overall shape is described using four parameters, with the following
values:

- The width :math:`w = 4` m;
- The height :math:`h = 2` m;
- The distance :math:`d = 1` m;
- The angle :math:`a = 100^\circ`.

The materials used in this cross section are listed in
:numref:`Table %s <tutorial_materials_iso>` and
:numref:`Table %s <tutorial_materials_ortho>`.
The layups used in this cross section are listed in
:numref:`Table %s <tutorial_layups>`.

.. csv-table:: Isotropic material properties
  :name: tutorial_materials_iso
  :header-rows: 2
  :align: center

  "Name", "Density", :math:`E`, :math:`\nu`
   , |den_si|, |mod_si_k|,
  "m0", 1.00, 25.00, 0.30

.. tabularcolumns:: |l|r|r|r|r|r|r|r|r|r|r|

.. csv-table:: Orthotropic material properties
  :name: tutorial_materials_ortho
  :header-rows: 2
  :align: center

  "Name", "Density", |e1|, |e2|, |e3|, |g12|, |g13|, |g23|, |nu12|, |nu13|, |nu23|
   , |den_si_k|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, |mod_si_g|, , ,
  "m1", 1.86, 37.00, 9.00, 9.00, 4.00, 4.00, 4.00, 0.28, 0.28, 0.28
  "m2", 1.83, 10.30, 10.30, 10.30, 8.00, 8.00, 8.00, 0.30, 0.30, 0.30

.. csv-table:: Layups
  :name: tutorial_layups
  :header-rows: 2
  :align: center

  "Component", "Name", "Material", "Ply thickness", "Orientation", "Number of plies"
  , , , "m", "degree",
  "Walls", "layup_1", "m1", 0.02,  45, 1
         ,          , "m1", 0.02, -45, 1
         ,          , "m2", 0.05,   0, 1
         ,          , "m1", 0.02,   0, 2
  "Webs", "layup_2", "m2", 0.05, 0, 1
        ,          , "m1", 0.02, 0, 3
        ,          , "m2", 0.05, 0, 1



Steps of preparing input files
------------------------------

In PreVABS, a cross section is composed of components, each of which
can either be a laminate or a fill. The laminate type component is
composed of segments with different layups. For a realistic cross section,
there may be several different ways to decompose it, which may need
different information in the input files to build the model.

Hence,
the first step is to decide a way of decomposition of the cross section.

For this example, the first step is trivial. The cross section can be
decomposed into three components: the walls, the webs, and the fill.

At the same time, the order of creating components should also be decided.
This is done by figuring out the dependence relationships between
components. For this example, the exact shape of each web depends on
the shape of the walls, and the shape of the fill depends on both the
webs and the walls. Then the order of creation should be: first creating
the walls, then the webs, and at last the fill, as shown in
:numref:`Fig. %s <fig_tutorial_box_order>`.

.. figure:: /figures/tutorial_box_order.png
  :name: fig_tutorial_box_order
  :width: 6in
  :align: center

  Order of components creation.

The next step is to prepare various input files based on all design
parameters listed above. In this example, all files are in the XML format.
A brief summary of these input files is listed below.

- A baseline file (*baselines.xml*), storing definitions of geometric
  elements.
- A material file (*MaterialDB.xml*), storing definitions of materials
  and laminae.
- A layup file (*layups.xml*), storing definitions of layups.
- A main cross section file (*box.xml*), storing definitions of components
  and other configurations of modeling and analysis.

For this tutorial, all files can have arbitrary file names and be placed at any working directory, except the material database, which must be named as *MaterialDB.xml* and placed at the same location as where the PreVABS executable is.

Another option is to use a local file in the working directory with an arbitrary name storing the material properties.
The requirement of using this local file is to explicitly provide the material file name in the main input file.
Please check Section: :ref:`section-overall`.

Prepare geometric elements
^^^^^^^^^^^^^^^^^^^^^^^^^^

As shown in :numref:`Fig. %s <fig_tutorial_box_points>`, seven points
are used to define the shape of the cross section. Points p1 to p4 define
the walls, p5 and p6 define the webs, and p0 indicates the space which
should be filled with some material. The origin of the coordinate system
is placed at the centroid of the rectangular. Based on the design parameters
:math:`w`, :math:`h` and :math:`d`, coordinates of all points are found
and listed in :numref:`Table %s <table_tutorial_box_points>`.

.. figure:: /figures/tutorial_box_points.png
  :name: fig_tutorial_box_points
  :width: 6in
  :align: center

  Key points defining the shape of the cross section.

.. csv-table:: Key points
  :name: table_tutorial_box_points
  :header-rows: 1
  :align: center

  "Name", "Coordinate"
  "p0", "(0, 0)"
  "p1", "(2, 1)"
  "p2", "(-2, 1)"
  "p3", "(-2, -1)"
  "p4", "(2, -1)"
  "p5", "(1, 0)"
  "p6", "(-1, 0)"

Base lines are created based on key points defined above. As shown in
:numref:`Fig. %s <fig_tutorial_box_lines>`, three lines are created.
Line 1 is defined by connecting the four points (p1 -> p2 -> p3 -> p4 -> p1).
Line 2 and 3 are defined by a single point with an incline angle. For
line 2, it is the point p5 with an angle of 100 degrees. For line 3, it is
the point p6 with an angle of 80 degrees.

The direction of each base line is important. It is related with how the
laminate is created for each segment, and how the local coordinate system
is defined for each element.

The completed input file for geometry is shown in
:numref:`Listing %s <code_tutorial_box_baselines>`.

.. figure:: /figures/tutorial_box_lines.png
  :name: fig_tutorial_box_lines
  :width: 6in
  :align: center

  Base lines defining the shape of the cross section.

.. code-block:: xml
  :linenos:
  :name: code_tutorial_box_baselines
  :caption: Input file for geometric elements (*baseline.xml*).

  <baselines>
    <basepoints>
      <point name="p0">0  0</point>
      <point name="p1">2  1</point>
      <point name="p2">-2  1</point>
      <point name="p3">-2  -1</point>
      <point name="p4">2  -1</point>
      <point name="p5">1  0</point>
      <point name="p6">-1  0</point>
    </basepoints>
    <baseline name="line1" type="straight">
      <points>p1,p2,p3,p4,p1</points>
    </baseline>
    <baseline name="line2" type="straight">
      <point>p5</point>
      <angle>100</angle>
    </baseline>
    <baseline name="line3" type="straight">
      <point>p6</point>
      <angle>80</angle>
    </baseline>
  </baselines>

Prepare materials and layups
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Material data are stored in the material database. As stated above, this
file must be named as *MaterialDB.xml* and placed at the directory where
the PreVABS executable is. The format of this file is shown in
:numref:`Listing %s <code_tutorial_box_materials>`. Arrangement of data
under the ``<elastic>`` element are different for different material
types, which can be isotropic, orthotropic, or anisotropic.

Another part of the file is the lamina data. A lamina is a unique combination
of material and ply thickness. For this example, according to the layup
table (::numref:`Table %s <tutorial_layups>`) given above, there are two
laminae. One has material m1 and thickness 0.02, and another one has
material m2 and thickness 0.05. It is the lamina, instead of the material,
that will be used to define each layer of the layup.

.. code-block:: xml
  :linenos:
  :name: code_tutorial_box_materials
  :caption: Input file for materials (*MaterialDB.xml*).

  <materials>
    <material name="m0" type="isotropic">
      <density>1.0</density>
      <elastic>
        <e>25.0e3</e>
        <nu>0.3</nu>
      </elastic>
    </material>
    <!-- =========================================================== -->
    <material name="m1" type="orthotropic">
      <density>1.86E+03</density>
      <elastic>
        <e1>3.70E+10</e1>
        <e2>9.00E+09</e2>
        <e3>9.00E+09</e3>
        <g12>4.00E+09</g12>
        <g13>4.00E+09</g13>
        <g23>4.00E+09</g23>
        <nu12>0.28</nu12>
        <nu13>0.28</nu13>
        <nu23>0.28</nu23>
      </elastic>
    </material>
    <lamina name="la_m1_002">
      <material>m1</material>
      <thickness>0.02</thickness>
    </lamina>
    <!-- =========================================================== -->
    <material name="m2" type="orthotropic">
      <density>1.83E+03</density>
      <elastic>
        <e1>1.03E+10</e1>
        <e2>1.03E+10</e2>
        <e3>1.03E+10</e3>
        <g12>8.00E+09</g12>
        <g13>8.00E+09</g13>
        <g23>8.00E+09</g23>
        <nu12>0.30</nu12>
        <nu13>0.30</nu13>
        <nu23>0.30</nu23>
      </elastic>
    </material>
    <lamina name="la_m2_005">
      <material>m2</material>
      <thickness>0.05</thickness>
    </lamina>
  </materials>

Layup information is stored in a separate file. Based on the layup table,
the input file can be prepared with the format shown in
:numref:`Listing %s <code_tutorial_box_layups>`. The order of the layers
defines the laying sequence from the base line. The number in the ``<layer>``
element stands for the orientation. If there is a colon, then the number
behind it stands for the number of plies in this layer. If there is no
number at all, then by default this layer has only one ply with orientation
of 0 degree.

.. code-block:: xml
  :linenos:
  :name: code_tutorial_box_layups
  :caption: Input file for layups (*layups.xml*).

  <layups>
    <layup name="layup1">
      <layer lamina="la_m1_002">45</layer>
      <layer lamina="la_m1_002">-45</layer>
      <layer lamina="la_m2_005">0</layer>
      <layer lamina="la_m1_002">0:2</layer>
    </layup>
    <layup name="layup2">
      <layer lamina="la_m2_005"></layer>
      <layer lamina="la_m1_002">0:3</layer>
      <layer lamina="la_m2_005"></layer>
    </layup>
  </layups>

Create components
^^^^^^^^^^^^^^^^^

There are two types of components in PreVABS, laminate and fill. For
this example, based on the decomposition we did at the begining of this
section, there are three laminate-type components and one fill-type
component. Besides, the sequence of creating components is important
as stated at the beginning of this section. This is defined by declaring
which components are needed before creating the current one.

Each laminate-type component is composed of one or more segments. Each
segment is a unique combination of a base line and a layup. The layup
can be created on either side of the base line. This is controlled by
an attribute ``direction``, which can be either left or right. This can
be understood as the left- or right-hand side when walking along the
base line, as shown in :numref:`Fig. %s <fig_tutorial_box_segments>`.

As for the ordering, the walls should be completed first, since its
inner boundary is needed to trim the base lines of both webs. Hence,
each web component depends on the walls component, as shown in
:numref:`Listing %s <code_tutorial_box_laminate>`.

.. figure:: /figures/tutorial_box_segments.png
  :name: fig_tutorial_box_segments
  :width: 6in
  :align: center

  Layup directions for each segment.

.. code-block:: xml
  :linenos:
  :name: code_tutorial_box_laminate
  :caption: Input elements for the laminate-type components

  <component name="walls">
    <segment>
      <baseline>line1</baseline>
      <layup>layup1</layup>
    </segment>
  </component>
  <component name="web1" depend="walls">
    <segment>
      <baseline>line2</baseline>
      <layup>layup2</layup>
    </segment>
  </component>
  <component name="web2" depend="walls">
    <segment>
      <baseline>line3</baseline>
      <layup direction="right">layup2</layup>
    </segment>
  </component>

The fill-type component is defined by a point and a material. Here, the
point p0 is used to indicate that the material should be filled in the
space in the middle enclosed by the walls and both webs. At the same
time, the dependent components are also decided, as shown in
:numref:`Listing %s <code_tutorial_box_fill>`.

.. figure:: /figures/tutorial_box_fill.png
  :name: fig_tutorial_box_fill
  :width: 6in
  :align: center

  The fill-type component.

.. code-block:: xml
  :linenos:
  :name: code_tutorial_box_fill
  :caption: Input elements for the fill-type component

  <component name="fill" type="fill" depend="walls,web1,web2">
    <location>p0</location>
    <material>m0</material>
  </component>

Set other configurations and complete the main input file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Besides the definitions of components, the main input file of the cross
section contains several other required or optional settings.

The first part is the ``<include>`` settings, which is required. This
contains names of the base lines and layups files.

The second part is the ``<analysis>`` settings, which is optional.
This contains configurations used by VABS for the cross-sectional analysis.
For this example, the ``<model>`` setting is set to 1, which means that
the Timoshenko beam model will be used and the 6x6 stiffness matrix will
be calculated.

The last part is the ``<general>`` settings, which is optional. This
part contains global configurations for the shape and meshing of the
cross section. Here, the global mesh size is set to 0.02.

The completed main input file for the cross section is shown in
:numref:`Listing %s <code_tutorial_box_main>`.

.. code-block:: xml
  :linenos:
  :name: code_tutorial_box_main
  :caption: Input file for the cross section

  <cross_section name="box">
    <include>
      <baseline>baselines</baseline>
      <layup>layups</layup>
    </include>
    <analysis>
      <model>1</model>
    </analysis>
    <general>
      <mesh_size>0.02</mesh_size>
    </general>
    <component name="walls">
      <segment>
        <baseline>line1</baseline>
        <layup>layup1</layup>
      </segment>
    </component>
    <component name="web1" depend="walls">
      <segment>
        <baseline>line2</baseline>
        <layup>layup2</layup>
      </segment>
    </component>
    <component name="web2" depend="walls">
      <segment>
        <baseline>line3</baseline>
        <layup direction="right">layup2</layup>
      </segment>
    </component>
    <component name="fill" type="fill" depend="walls,web1,web2">
      <location>p0</location>
      <material>m0</material>
    </component>
  </cross_section>


Execution and results
---------------------

Once all input files are prepared, the cross section can be created and
homogenized using the following command:

::

  prevabs -i box.xml -h -v -e

If everything works successfully, Gmsh will be called and the cross section
will be plotted as shown in :numref:`Fig. %s <fig_tutorial_box_plot>`
(the display of element edges is turned off in the figure for clarity),
and VABS homogenization analysis will be carried out and effective beam
properties can be found in the file ``box.sg.K``. The effective Timoshenko
stiffness matrix is listed in :numref:`Table %s <tutorial_stiffness>`.


.. figure:: /figures/tutorial_box.png
  :name: fig_tutorial_box_plot
  :width: 6.5in
  :align: center

  The cross section created by PreVABS and plotted by Gmsh.

.. csv-table:: Timoshenko stiffness matrix in the file *box.sg.K*
  :name: tutorial_stiffness
  :delim: space
  :align: center

   3.991E+10   -1.662E+05   -4.037E+01    4.204E+07   -4.358E+03    2.867E+01
  -1.662E+05    6.743E+09    3.945E+04   -2.918E+08   -1.577E+07   -4.150E+03
  -4.037E+01    3.945E+04    6.165E+09    8.220E+03   -2.897E+03   -8.700E+06
   4.204E+07   -2.918E+08    8.220E+03    1.972E+10    2.721E+05    3.303E+02
  -4.358E+03   -1.577E+07   -2.897E+03    2.721E+05    2.173E+10   -3.025E+04
   2.867E+01   -4.150E+03   -8.700E+06    3.303E+02   -3.025E+04    6.728E+10
