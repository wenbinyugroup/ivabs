.. include:: replace.txt

.. _section-shape:

Geometry and shapes
===================



Base points
...........

Base points are used to draw base lines, which form the skeleton of a cross section. They can be either actually on the *Base line*\ s, or not, as reference points, for example the center of a circle. Points that are directly referred in the definitions of *Base line*\ s are called *Key point*\ s, such as starting and ending points of a line or an arc, or the center of a circle. The rest are *Normal point*\ s. The coordinates provided in the input file are defined in the basic frame **z** and then transformed into the cross-sectional frame **x**, through processes like translating, scaling and rotating. If none of those operations are needed, then those data also define the position of each point in the frame **x**.

The file storing these data is a plain text file, with a file extension ``.dat``. This block of data has three columns and *n* rows, where *n* is the number of *Base point*\ s. The three columns are arranged as ::

  label  z2  z3

where the first column is the labels/names for each point, and the second and the third columns are the |z2| and |z3| coordinates, respectively. Some notes for this input file are:

- Three columns are separated by spaces;
- ``label`` can be the combination of any letters, numbers and underscores "_";
- Each *Key point*\ 's name must be unique; 
- Meaningful names for *Key point*\ s are highly recommended;
- *Normal point*\ s' names can be less meaningful, even identical;
- The order of the point list is important for those points belonging to a sublist defining the direction of a *Base line*, but it can be placed in any part of the big list.

Base lines
..........

*Base line*\ s form the skeleton of a cross section. PreVABS can handle three types of *Base line*\ s, straight, arc and circle, as shown in :numref:`Fig. %s <fig_baselinetypes>`. Spline are approximated by straight lines. Some types have several ways to define the *Base line*. In the end, all curved *Base line*\ s are converted into a chain of short straight lines in PreVABS. User can provide those short straight lines directly for spline, arc and circle. Or, for arc or circle, user can use simple rules to draw the shape first and then PreVABS will discretize it.

Data for *Base line*\ s are stored in an XML formatted file. The general arrangement of data is shown in :numref:`Listing %s <code_baseline_template>`. All *Base line* definitions are stored in the root element ``<baselines>``, which has one attribute ``basepoints`` indicating the name of *Base point* file used in this cross section. Each ``<baseline>`` element is the definition of a *Base line*. Each one has a unique ``name`` and a ``type``, which can be ``straight``, ``arc`` or ``circle``. Inside the ``baseline`` element, the ``straight`` and ``arc`` types have several different ways of definition, and thus the arrangements of data are different, which will be explained in details below.

.. figure:: figures/baselinetypes.png
  :name: fig_baselinetypes
  :width: 6in
  :align: center

  Three types of *Base line*\ s in PreVABS.

.. code-block:: xml
  :linenos:
  :name: code_baseline_template
  :caption: *Base line* input file template.

  <baselines basepoints="basepoints">
    <baseline name="name1" type="straight">...</baseline>
    <baseline name="name2" type="arc">...</baseline>
    <baseline name="name3" type="circle">...</baseline>
    ...
  </baselines>

Straight
~~~~~~~~

For the *Straight* type, the basic idea is to provide *Key point*\ s for the chain of straight lines and the direction of the *Base line* is defined by the order of the point list, as shown in :numref:`Fig. %s <fig_baselinestraight>`. Spline is also defined in this way. Some notes are:

- All *Key point*\ s are placed in the ``<points>`` element;
- *Key point*\ s are separated by comma;
- Successive points can be included using two *Key point*\ s separated by colon;
- Space is not allowed;
- Above two methods can be used in combination.

.. note:: Use ``type="straight"`` for splines.

Besides, a simple straight line like (i) in :numref:`Fig. %s <fig_baselinestraight>` can also be defined using one *Key point* and an angle, which is shown as (iv) in the same figure. In this case, PreVABS will calculate the second *Key point* (a') and generate the *Base line*. Some notes are:

- Two elements are used here, ``<point>`` and ``<angle>``. The former element stores the user-provided *Key point* "a", and the latter element stores the angle "theta";
- The positive angle (degree) is defined from the positive |z2| axis, counterclockwise;
- The PreVABS-computed second *Key point* will always be "not lower" than the user-provided *Key point*, which means the *Base line* will always be pointing to the upper left or upper right, or to the right if it is horizontal;
- The two *Key point*\ s do not indicate the two ends of the *Base line*; or, in other words, *Base line* defined in this way is infinite.

For the four *Base line*\ s in :numref:`Fig. %s <fig_baselinestraight>`, the sample input file is shown in :numref:`Listing %s <code_baseline_straight>`, assuming that there is a *Base point* file named "basepoints.dat" in the same folder.

.. figure:: figures/baselinestraight.png
  :name: fig_baselinestraight
  :width: 100%
  :align: center

  Different ways of defining *Straight* *Base line*\ s in PreVABS.

.. code-block:: xml
  :linenos:
  :name: code_baseline_straight
  :caption: Sample input file for the *Base line*\ s shown in :numref:`Fig. %s <fig_baselinestraight>`

  <baselines basepoints="basepoints">
    ...
    <baseline name="i" type="straight">
      <points>a,z</points></baseline>
    <baseline name="ii" type="straight">
      <points>a,b,c,z</points></baseline>
    <baseline name="iii" type="straight">
      <points>a:z</points></baseline>
    <baseline name="iv" type="straight">
      <point>a</point><angle>theta</angle></baseline>
    ...
  </baselines>

Arc
~~~

A real arc can also be created using a group of *Base point*\ s, in which case the *Straight* type should be used. The *Arc* type provides a parametric way to build this type of *Base line*, then PreVABS will discretize it. To uniquely define an arc, user needs to provide at least four of the following six items: center, starting point, ending point, radius, angle and direction, as shown in :numref:`Fig. %s <fig_baselinearc>`. Two possible ways of defining an arc are given in :numref:`Fig. %s <fig_baselinearc2>`, where the first one is defined by center, starting point, ending point and direction, and the second one is defined by center, starting point, angle and direction.

For preparing the input file, some notes are:

- Element tags used for arc are ``<center>``, ``<start>``, ``<end>``, ``<radius>``, ``<angle>`` and ``<direction>``;
- Not used elements should be deleted;
- ``<center>``, ``<start>`` and ``<end>`` store the *Key point* labels from the *Base point* file;
- ``<angle>`` stores the angle in degrees greater than 0 and less than 360;
- ``<direction>`` can only be ``cw`` for clockwise or ``ccw`` for counterclockwise. ``ccw`` is the default.

.. note:: ``<radius>`` is ignored in the current version, and will be supported in a future version.

A sample input file for the two arcs shown in :numref:`Fig. %s <fig_baselinearc2>` is provided in :numref:`Listing %s <code_baseline_arc>`.

.. figure:: figures/baselinearc.png
  :name: fig_baselinearc
  :width: 6in
  :align: center

  Items in an arc.

.. figure:: figures/baselinearc2.png
  :name: fig_baselinearc2
  :width: 6in
  :align: center

  Two possible cases of defining an arc.

.. code-block:: xml
  :linenos:
  :name: code_baseline_arc
  :caption: Sample input file for the *Base line*\ s shown in :numref:`Fig. %s <fig_baselinearc2>`

  <baselines basepoints="basepoints">
    ...
    <baseline name="left" type="arc">
      <center>c</center>
      <start>s</start>
      <end>e</end>
      <direction>ccw</direction>
    </baseline>
    <baseline name="right" type="arc">
      <center>c</center>
      <start>s</start>
      <angle>a</angle>
      <!-- here the direction is the default value 'ccw' -->
      </baseline>
    ...
  </basepoints>

Circle
~~~~~~

Defining a circle is simpler than an arc. User only need to provide a center with radius or another point on the circle. The corresponding element tags are ``<center>``, ``<radius>`` and ``<point>``. A sample input file demonstrating the two methods is presented in :numref:`Listing %s <code_baseline_circle>`.

.. code-block:: xml
  :linenos:
  :name: code_baseline_circle
  :caption: Sample input file for circles.

  <baselines basepoints="basepoints">
    ...
    <baseline name="circle1" type="circle">
      <center>c</center>
      <radius>r</radius>
    </baseline>
    <baseline name="circle2" type="circle">
      <center>c</center>
      <point>p</point>
    </baseline>
    ...
  </baselines>

