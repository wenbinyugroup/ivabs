.. include:: replace.txt

Prepare Cross Section
=====================

In PreVABS, a cross section is defined through three aspects: geometry, material and overall configuration, as shown in :numref:`Fig. %s <fig_csfiles1>`. The geometry aspect comprises definitions of base points and base lines. The material aspect includes material properties, lamina thicknesses, layup stacking sequences, etc. The overall configuration defines the general size of the cross section, position of the coordinate origin, mesh size and element type of the finite element model.

.. figure:: figures/chart1.png
  :name: fig_csfiles1
  :width: 50%
  :align: center
  
  Cross section definition in PreVABS.

In PreVABS, the key to preparing input files for a cross section is defining *Segment*\ s. A *Segment* is a unique combination of a *Base line* and a *Layup*, as shown in :numref:`Fig. %s <fig_airfoil1>`. Another important concept is *Level*, which collects segments into different groups based on how they connect to each other. For regions like the leading and trailing edges of an airfoil, it is sometimes difficult to handle. PreVABS treats these *Connection*\ s separately and thus requires separate declarations of these joints between segments. More details about these concepts can be found in :numref:`Section %s <section-basepoint-line>`, :numref:`Section %s <section-material-layup>` and :numref:`Section %s <section-segment>`.

.. figure:: figures/airfoil.png
  :name: fig_airfoil1
  :width: 100%
  :align: center

  Basic components in a typical cross section.

To prepare the cross section, five input files are needed. Definitions of *Base point*\ s, *Base line*\ s, *Material*\ s and *Layup*\ s are stored in four input files separately. A top level *Cross section* file stores the definitions of *Segment*\ s and *Connection*\ s, overall configurations and references to other files. Except the *Base point*\ s file, which has a file extension .dat, all other files use an XML format.

.. toctree::
    :maxdepth: 3
    :caption: Subtopics

    pre_coordinate
    pre_shape
    pre_material
    pre_segment
    pre_others
    pre_overall
    pre_recover


