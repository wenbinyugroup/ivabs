.. include:: replace.txt

.. _section-segment:

Segments and Connections
------------------------

*Segment* is the key to a cross section in PreVABS. A schematic plot is shown in :numref:`Fig. %s <fig_segment>`. A *Segment* is a unique combination of *Base line* and *Layup*. The *Base line* provides a reference for the position and direction of the *Layup*. *Layers* can be laid to the left or right of the *Base line*. The direction is defined as one's left or right, assuming one is walking along the direction of the *Base line*.

*Connection* or *Joint* is another key aspect. There are three types of *Connection*\ s considered in PreVABS, as shown in :numref:`Fig. %s <fig_joints>`, two types of "V" shape and one of "T" shape. "V" shape *Connection* is the one that two *Segment*\ s are joint end to end, while in "T" shape *Connection*, two *Segment*\ s are joint end to side. Two "V" shape *Connection*\ s produce different geometries when the thicknesses of two connected *Segment*\ s are different. The first type tries to remove the step in the *Joint* region, while the second type uses a bisector as the interface of two *Segment*\ s, which will create a step. By default, all *Connection*\ s have the "V2" shape. In the current version of PreVABS, the "V1" type is used for four specific groups of cross sections, "box", "L", "C" and "Z". In this case, user needs to specify the name of the cross section as "box", "L", "C" or "Z". More details about the ``name`` and other attributes of a cross section can be found in :numref:`Section %s <section-overall>`.

*Level* of a *Segment* is used for dealing with structures with "T" shape connections, such as the web in an airfoil cross section. Since PreVABS does not require users to define connections types explicitly, this "T" shape joint is realized by putting *Segment*\ s into groups with different building priorities. The smaller the *Level* number is, the higher the priority will be. Group with the highest priority will be created first. Then *Segment*\ s in the lower group will be built and connected to the previous group using the "T" type *Joint*.

.. figure:: figures/segment.png
  :name: fig_segment
  :width: 6in
  :align: center

  A typical *Segment* in PreVABS and the relation between *Base line* direction and *Layup* direction.

.. figure:: figures/joints.png
  :name: fig_joints
  :width: 6in
  :align: center

  Three types of *Connection*\ s that can be created in PreVABS.

All *Segment*\ s and *Connection*\ s information are stored in a main input file. The complete format will be discussed later since the overall configurations are also included in this file, which will be explained in :numref:`Section %s <section-overall>`. A template for *Segment*\ s and *Connection*\ s are given in :numref:`Listing %s <code_segments>`. All *Segment*\ s are placed in a single element ``<segments>``. Each ``<segment>`` element has two attributes, ``name`` and ``level``, and two child elements, ``<baseline>`` and ``<layup>``. The ``<layup>`` element has another attribute ``direction`` (see :numref:`Fig. %s <fig_segment>`). Some notes are:

- ``level`` can be any positive integers;
- The first ``level`` number must be 1 always;
- ``level`` numbers do not need to be consecutive. For example, the first ``level`` is 1 and the next ``level`` number can be 10;
- ``direction`` of a ``layup`` element can only be ``left`` or ``right``;

Some extra notes regarding to the usage of *Connection* and *Level* are:

- In the current version of PreVABS, ``<connections>`` is used for defining leading and/or trailing edge in an airfoil only, and works only if the type of the cross section is ``airfoil``.
- Defining leading and/or trailing edge in ``<connections>`` is for handling the complex (sharp, narrow, highly different layups) shapes of these two joints. If the shape is not complex, then users do not need to make these definitions, and the running time of PreVABS will be less.
- Creating shear webs in an airfoil cross section is the main purpose of the *Level* attribute. Hence, similar to this, a "web" in a ``general`` type cross section can also be defined this way.

.. code-block:: xml
  :linenos:
  :name: code_segments
  :caption: A template for the *Segment*\ s and *Connection*\ s in a main input file.

  <segments>
    <segment name="segment1" level="1">
      <baseline>baseline1</baseline>
      <layup direction="right">layup1</layup>
    </segment>
    <segment name="segment2" level="10">
      <baseline>baseline2</baseline>
      <layup direction="left">layup2</layup>
    </segment>
    ...
  </segments>
  <connections>
    <connection name="leading_edge">
      <segment>segment1</segment>
      <segment>segment2</segment>
    </connection>
    <connection name="trailing_edge">
      <segment>segment3</segment>
      <segment>segment4</segment>
    </connection>
    ...
  </connections>

