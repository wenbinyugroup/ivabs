.. _section-component:

Components
==========

.. code-block:: xml
  :linenos:
  :name: code_component
  :caption: Input syntax for components.

  <component name="" type="" depend="">...</component>

**Specification**

- **<component>** - Root element for the definition of each component.

  - *name* - Name of the component.
  - *type* - Type of the component. Choose one from 'laminate' and 'fill'. Default is 'laminate'.
  - *depend* - List of name of dependent components, delimited by commas.










Laminate-type component
-----------------------

For a cross section in PreVABS, laminates are created as segments.
A segment is a unique combination of a base line and a layup.
Segments are connected through different ways as shown in :numref:`Fig. %s <fig_joints>`.
According to this, segments can be grouped into components.
The rule of thumb is: if two segments are connected in the first two ways ('V1' and 'V2'), then they belong to one component; if they are connected as the third way ('T'), then they should be put into different components, and component 2 will be created after the finish of component 1.

.. figure:: /figures/joints.png
  :name: fig_joints
  :width: 6in
  :align: center

  Three types of connections that can be created in PreVABS.

A schematic plot of a segment is shown in :numref:`Fig. %s <fig_segment>`.
The base line provides a reference for the position and direction of the layup.
Layers can be laid to the left or right of the base line.
The direction is defined as one's left or right, assuming one is walking along the direction of the base line.

.. figure:: /figures/segment.png
  :name: fig_segment
  :width: 6in
  :align: center

  A typical segment in PreVABS and the relation between base line direction
  and layup direction.

All segments definitions are stored in the main input file.
The complete format will be discussed later since the overall configurations are also included in this file, which will be explained in Section: :ref:`section-overall`.
The input syntax for laminate-type components are given in :numref:`Listing %s <code_segments>`.
Each component can have multiple segments.

There are two ways to define segments.

DEFINITION 1: Define segments individually
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use a base line and a single layup to create the segment.
In this way, the layup covers the entire of the base line.
Each ``<segment>`` element has one attribute, ``name``, and two child elements, ``<baseline>`` and ``<layup>``.
The ``<layup>`` element has another attribute ``direction`` (see :numref:`Fig. %s <fig_segment>`).

Joint of two connecting segments can be changed from 'V2' (default) to 'V1' by using a ``<joint>`` element.
It requires the names of two segments, delimited by a comma (',') and an attribute ``style`` specifying the joint type.

DEFINITION 2: Define segments collectively
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use a base line and multiple layups to create multiple segments.
Each layup can be assigned to a portion of the base line, using a beginning and an ending locations.
These locations are normalized parametric positions on the base line.
The beginning location must be smaller than the ending one.
If the line is open, the location can only be a number between 0 and 1.
If the line is closed, the location can be any number, even negative, as long as the length is not greater than 1.
Then PreVABS will split the base line, combine layups and create segments automatically.

An example is provided below (:numref:`Fig %s <fig-param-layup-example-define>`, :numref:`Fig %s <fig-param-layup-example-plot>`, :numref:`Listing %s <code-param-layup-example>`).


.. code-block:: xml
  :linenos:
  :name: code_segments
  :caption: Input syntax for the laminate-type components.

  <component name="cmp_surface">
    <segment name="sgm_1">
      <baseline> baseline1 </baseline>
      <layup direction="right"> layup1 </layup>
    </segment>
    <segment name="sgm_2">
      <baseline>...</baseline>
      <layup>...</layup>
    </segment>
    ...
    <joint style="2"> sgm_1,sgm_2 </joint>
    ...
  </component>


  <component name="cmp_web">
    <segment>
      <baseline> baseline2 </baseline>
      <layup direction="left"> layup2 </layup>
    </segment>
    ...
  </component>


  <component name="...">
    <segments>
      <baseline> base_line_3_name </baseline>
      <layup_side> left </layup_side>
      <layup> layup_1_name </layup>
      <layup begin="0.1"> layup_2_name </layup>
      <layup end="0.7"> layup_3_name </layup>
      <layup begin="0.2" end="0.9"> layup_4_name </layup>
      ...
    </segments>
  </component>


Example
"""""""

.. _fig-param-layup-example-define:

.. figure:: /figures/param_layup_example_design.png
  :width: 4in
  :align: center

  Segment layup range definition.


.. _fig-param-layup-example-plot:

.. figure:: /figures/param_layup_example_plot.png
  :width: 3in
  :align: center

  Segments plot.




.. _code-param-layup-example:

.. code-block:: xml
  :linenos:
  :caption: Example input.

  <component name="...">
    <segments>
      <baseline> l </baseline>
      <layup> layup1 </layup>
      <layup begin="0.2" end="0.75"> layup2 </layup>
      <layup begin="-0.1" end="0.5"> layup3 </layup>
      <layup begin="-0.6" end="-0.2"> layup4 </layup>
    </segments>
  </component>




**Specification**

*DEFINITION 1*

- **<segment>** - Root element of the definition of the segment.

  - *name* - Name of the segment.

- **<baseline>** - Name of the base line defining this segment.
- **<layup>** - Name of the layup defining this segment.

  - *direction* - Direction of layup. Choose one from 'left' and 'right'. Default is 'left'.

- **<joint>** - Names of two segments delimited by a comma (',') that will be joined.

  - *style* - Style of the joint. Choose one from '1' and '2'. Default is '1'.


*DEFINITION 2*

- **<segments>** - Root element of the definition.
- **<baseline>** - Name of the base line definint these segments.
- **<layup_side>** - Direction of the following layups. Choose one from 'left' and 'right'. Default is 'left'.
- **<layup>** - Name of the layup.

  - *begin* - Normalized parametric beginning location of the layup on the base line. Defualt is '0.0'.
  - *end* - Normalized parametric ending location of the layup on the base line. Defualt is '1.0'.



















Fill-type component
-------------------

Besides creating laminates, user can use one material to fill a region.
A typical usage is a nose mass in an airfoil type cross section.
A schematic plot is shown in :numref:`Fig. %s <fig_filling1>`.

The key to this type of component is the indication of the fill region.
There are two things to pay attention to.
First, make sure that the boundary of the region is well-defined.
The region can be surrounded by a number of components.
User can also create some extra base lines as new boundaries.
Second, locate the region where the material will be filled into.
Then can be done by using a point inside the region, or if there are extra base lines, user can indicate the fill side with respect to one of the lines, similar to defining layup side in a segment.

Fill-type components are also defined in the main input file.
A template is shown in :numref:`Listing %s <code_fillings>`.
A fill-type component is indicated by the attribute ``type="fill"``.
A ``<material>`` child element is required.
A ``<baseline>`` element is optional and is used to create extra boundaries.
This sub-element has one attribute ``fillside``, which can be either left or right.
A ``<location>`` element is used to store the name of a point that is inside the desired fill region, and is also optional.

.. figure:: /figures/filling1.png
  :name: fig_filling1
  :width: 6in
  :align: center

  Example usage of a fill-type component as a nose mass in an airfoil
  cross section.

.. code-block:: xml
  :linenos:
  :name: code_fillings
  :caption: Input syntax for the fill-type components.

  <component name="cmp_fill_1" type="fill">
    <location> point_fill </location>
    <material> material1 </material>
  </component>


  <component name="cmp_fill_2" type="fill">
    <baseline> bsl </baseline>
    <location> point_fill </location>
    <material> material1 </material>
    <mesh_size at="p1,p2"> 0.1 </mesh_size>
  </component>


  <component name="cmp_fill_3" type="fill">
    <baseline fillside="right"> bsl_3 </baseline>
    <material> material1 </material>
  </component>





Local mesh size
^^^^^^^^^^^^^^^

Besides the mesh size set globally in the main input file, filling type components can be assigned local mesh sizes.
This is usually for the purpose of reducing the total number of elements and computational cost.
This feature is based on the embedded objects (points and lines) provided by Gmsh.
Hence, one or more points need to be specified as the 'seed' of local mesh sizes.

.. code-block:: xml

  <mesh_size at="p1,p2">0.1</mesh_size>

The mesh size will vary gradually from the local to the global setting.
Hence, if only one point is used, then the local mesh size will only affect a circular region.
If multiple points are used, then lines will be created by connecting points seqentially and assigned the local mesh size as well.

An example is provided below (:numref:`Fig %s <fig-local-mesh-example-define>`, :numref:`Fig %s <fig-local-mesh-example-plot>`, :numref:`Listing %s <code-local-mesh-example>`).



.. _fig-local-mesh-example-define:

.. figure:: /figures/local_mesh_define_mark.png
  :width: 3in
  :align: center

  Local mesh definition.


.. _fig-local-mesh-example-plot:

.. figure:: /figures/local_mesh.png
  :width: 3in
  :align: center

  Local mesh plot.




.. _code-local-mesh-example:

.. code-block:: xml
  :linenos:
  :caption: Example input.

  <component name="filling 1" type="fill" depend="...">
    <location> A </location>
    <material> material1 </material>
    <mesh_size at="A"> 0.2 </mesh_size>
  </component>

  <component name="filling 2" type="fill" depend="...">
    <location> B </location>
    <material> material2 </material>
    <mesh_size at="B,C"> 0.2 </mesh_size>
  </component>











**Specification**

- **<material>** - Name of the material to be filled. Required.
- **<location>** - Name of the point located in the fill region. Optional.
- **<baseline>** - Name of the base line defining part or complete boundary. Optional.

  - *fillside* - Side of the fill with respect to the base line. Optional.

- **<theta1>** - Rotating angle in degree about the |x1| axis. Optional. Default is 0 degree.
- **<theta3>** - Rotating angle in degree about the |y3| axis. Optional. Default is 0 degree.

- **<mesh_size>** - Local mesh size. Optional.

  - *at* - A list of names of points where the local mesh size will be assgined. Required.










Components dependency
---------------------

If two components are connected in the 'T' type (:numref:`Fig. %s <fig_joints>`), then the order of creation of the two components must be specified.
This is done by specifying the dependency.
For the case shown in the figure, the creation of the thin vertical component (purple) is dependent on the creation of the thick horizontal component (blue).
Hence, in the definition of the purple component, a ``depend`` attribute should be specified as shown below.

.. code-block:: xml
  :linenos:
  :name: code_depend
  :caption: Dependency.

  <component name="cmp_blue" type="laminate">...</component>
  <component name="cmp_purple" type="laminate" depend="cmp_blue">...</component>

If a component is dependent on multiple components, their names shoule all be listed, delimited by comma.




