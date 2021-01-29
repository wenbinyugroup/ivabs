.. include:: replace.txt

Guide for Preparing Input Files
===============================

In PreVABS, a cross section is defined through two aspects: components
and global configuration, as shown in :numref:`Fig. %s <fig_csfiles1>`.
Components are built from geometry and materials
The geometry aspect comprises definitions of base points and base lines.
The material aspect includes material properties, lamina thicknesses,
layup stacking sequences, etc. The global configuration contains the
files included, transformation, meshing options, and analysis settings.

.. figure:: figures/chart1.png
  :name: fig_csfiles1
  :width: 75%
  :align: center

  Cross section definition in PreVABS.

.. In PreVABS, the key to preparing input files for a cross section is
.. defining *Segment*\ s. A *Segment* is a unique combination of a
.. *Base line* and a *Layup*, as shown in :numref:`Fig. %s <fig_airfoil1>`.
.. Another important concept is *Level*, which collects segments into
.. different groups based on how they connect to each other. For regions
.. like the leading and trailing edges of an airfoil, it is sometimes
.. difficult to handle. PreVABS treats these *Connection*\ s separately
.. and thus requires separate declarations of these joints between segments.
.. More details about these concepts can be found in :ref:`section-shape`,
.. :ref:`section-material-layup` and :ref:`section-component`.

.. .. figure:: figures/airfoil.png
..   :name: fig_airfoil1
..   :width: 100%
..   :align: center

..   Basic components in a typical cross section.

To create the cross section, at least four input files are needed.
Definitions of the geometry, materials and layups are stored in three files separately.
A top level cross section file stores the definitions of components and global configurations.
In some cases, a separate file storing base points is needed (such as an airfoil).
Except the base points file, which has a file extension .dat, all other files use an XML format.


A top level cross section file stores all information that will be discussed in the following sections.
The input syntax for this main file is shown in :numref:`Listing %s <code_crosssection>`.

.. code-block:: xml
  :linenos:
  :name: code_crosssection
  :caption: Input syntax for the cross section file.

  <cross_section name="" format="">
    <include>...</include>
    <analysis>...</analysis>
    <general>...</general>
    <component>...</component>
    <component>...</component>
    ...
  </cross_section>

**Specification**

- **<cross_section>**

  - *name*
  - *format*

- **<include>**
- **<analysis>**
- **<general>**
- **<baselines>**
- **<layups>**
- **<component>**
- **<recover>**




.. toctree::
    :maxdepth: 2
    :caption: Subtopics

    pre_coordinate
    pre_shape
    pre_material
    pre_component
    pre_recover
    pre_overall


