.. _section-prevabs_guide:

Guide for Preparing Input Files
===============================

In PreVABS, a cross section is defined through two aspects: components and global configuration, as shown in :numref:`Fig. %s <fig_csfiles1>`.
Components are built from geometry and materials.
The geometry aspect comprises definitions of base points and base lines.
The material aspect includes material properties, lamina thicknesses, layup stacking sequences, etc. The global configuration contains the files included, transformation, meshing options, and analysis settings.

.. figure:: /figures/chart1.png
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
    <baselines>...</baselines>
    <layups>...</layups>
    <component>...</component>
    <component>...</component>
    ...
  </cross_section>


Data of geometry and layup can be arranged in two ways, controlled by the attribute ``format``:

* If omitted or set to 0, then the code will look for definitions of shapes and layups in separated files, specified in the element ``<include>``.
* If set to 1, then the code will look for the definitions in the current main input file.


**Specification**

- **<cross_section>**

  - *name* - Name of the cross-section.
  - *format* - Format of the input file. See explaination above.

- **<include>** - File names of separately stored data.
- **<analysis>** - Configurations of cross-sectional analysis.
- **<general>** - Overall settings of the cross-section.
- **<baselines>** - Definitions of geometry and shape.
- **<layups>** - Definitions of layups.
- **<component>** - Definitions of cross-sectional components.
- **<recover>** - Inputs for recovery.




.. toctree::
    :maxdepth: 2
    :caption: Subtopics

    guide/pre_coordinate
    guide/pre_shape
    guide/pre_material
    guide/pre_component
    guide/pre_recover
    guide/pre_overall


