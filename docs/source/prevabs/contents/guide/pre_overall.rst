.. include:: /replace.txt

.. _section-overall:

Other input settings
====================

There are three groups of these settings.

Included files
--------------

This part contains file names for base lines, materials (local) and layups as shown in :numref:`Listing %s <code_include>`.
The ``<material>`` sub-element is optional.
If this is included, PreVABS will read extra materials from this local file, besides the global material database (MaterialDB.xml).
If there are materials and laminae with the same names, data in the local material file will overwrite those in the global database.

- ``path`` in the ``<include>`` element is the relative path to the main input file;
- File extensions ``.xml`` can be omitted.

.. code-block:: xml
  :linenos:
  :name: code_include
  :caption: Input syntax for the included files.

  <include>
    <baseline> path/baseline_file_name </baseline>
    <material> path/material_file_name </material>
    <layup> path/layup_file_name </layup>
  </include>

**Specification**

- **<baseline>** - Name of the included base line file.
- **<material>** - Name of the included local material file.
- **<layup>** - Name of the included layup file.










Analysis options
----------------

The second part contains settings for the analysis in VABS.
``<model>`` can be 0 for classical beam model, or 1 for refined (Timoshenko) model.

.. code-block:: xml
  :linenos:
  :name: code_analysis
  :caption: A template for the analysis options in a main input file.

  <analysis>
    <model> 1 </model>
  </analysis>

**Specification**

- **<model>** - Beam model. Choose one from '0' (classical) and '1' (refined/Timoshenko).










Global shape and mesh settings
------------------------------

The last part contains optional global geometry and meshing settings, which are all stored in a ``<general>`` sub-element.

User can set the global transformations of the cross section.
The three transformation operations have been discussed in Section: :ref:`section-coordinate`.

- The order of transformation operation is: translating, scaling, and rotating;
- All operations are performed on the cross section, not the frame;
- The scaling operation will only scale the shape (base lines), and have
  no effect on the thicknesses of laminae;
- The rotating angle starts from the positive half of the |x2| axis,
  and increases positively counter-clockwise (right-hand rule).

There are two meshing options available now, global meshing size
``<mesh_size>`` and type of elements ``<element_type>``.

- If not setting, the global meshing size will be the minimum layer
  thickness by default;
- Two options for the element type are linear and quadratic.

.. code-block:: xml
  :linenos:
  :name: code_general
  :caption: A template for the global shape and mesh settings in a main input file.

  <general>
    <translate> e2  e3 </translate>
    <scale> scaling_factor </scale>
    <rotate> angle </rotate>
    <mesh_size> a </mesh_size>
    <element_type> quadratic </element_type>
    <tolerance> 1e-9 </tolerance>
  </general>

**Specification**

- **<translate>** - Horizontal and vertical translation of the cross-section. The origin will be moved to (-e2, -e3).
- **<scale>** - Scaling factor of the cross-section.
- **<rotate>** - Rotation angle of the cross-section.
- **<mesh_size>** - Global mesh size.
- **<element_type>** - Order of elements. ``linear`` or ``quadratic`` (default).
- **<tolerance>** - Tolerance used in geometric computation. Optional. Default value is 1e-12.

.. note:: Only triangular element is available in the current version.



