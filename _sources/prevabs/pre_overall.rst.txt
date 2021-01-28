.. include:: replace.txt

.. _section-overall:

Overall configurations
----------------------

The overall configurations contain two parts. First, user needs to tell PreVABS what the rest input files are, the *Base line* file, the *Material* file, and the *Layup* file. Second, user needs to set the overall geometry and meshing parameters, including three transformation operations, mesh size and element type. The three transformation operations have been discussed in :numref:`Section %s <section-coordinate>`. Although the two frames **z** and **x** have some distances between them, the *Translate* operation will actually move the geometry, instead of the coordinate system. Also, since the *Scale* operation is done in the second place, the absolute distances of translation are defined in the initial frame **z**. The rotation angle is counted from the positive direction of |x2| and follows the right-hand rule.

These overall configurations are also stored in the main input file. A template is shown in :numref:`Listing %s <code_overall>`. All included files are placed in the ``<include>`` element. The geometry and meshing configurations are placed in the ``<general>`` element. Some notes are:

- ``path`` in the ``<include>`` element is the relative path to the main input file;
- File extensions ``.xml`` can be omitted;
- ``e2`` and ``e3`` are distances before scaling. Default is (0.0, 0.0) if omitted;
- Default for ``<scale>`` is 1.0 if omitted;
- Default for ``<rotate>`` is 0.0 if omitted;
- ``<mesh_size>`` is defined globally. The default size is the smallest thickness of layers used in the cross section;
- ``<element_type>`` can only be ``linear`` or ``quadratic`` (default).

.. note:: Only triangular element is available in the current version.

.. code-block:: xml
  :linenos:
  :name: code_overall
  :caption: A template for the overall configurations in a main input file.

  <include>
    <baseline>path/baseline_file_name</baseline>
    <material>path/material_file_name</material>
    <layup>path/layup_file_name</layup>
  </include>
  <general>
    <translate>e2  e3</translate>
    <scale>scaling_factor</scale>
    <rotate>angle</rotate>
    <mesh_size>a</mesh_size>
    <element_type>quadratic</element_type>
  </general>

A top level *Cross section* file stores all information discussed in this and previous  sections. A template for this file is shown in :numref:`Listing %s <code_crosssection>`. The root element ``<cross_section>`` has two attributes, ``name`` (required) and ``type`` (optional), and four child elements, ``<include>``, ``<general>``, ``<segments>`` and ``<connections>``. Some notes are:

- ``name`` will be used in file names of PreVABS outputs. For example, the ``name`` in the template is ``cs1``, then the generated VABS input file name will be ``cs1_vabs.dat`` and Gmsh file name will be ``cs1.msh``;
- ``type`` can only be ``general`` (default) or ``airfoil``;

.. code-block:: xml
  :linenos:
  :name: code_crosssection
  :caption: A template for the *Cross section* file.

  <cross_section name="cs1" type="airfoil">
    <include>...</include>
    <general>...</general>
    <segments>...</segments>
    <connections>...</connections>
  </cross_section>



