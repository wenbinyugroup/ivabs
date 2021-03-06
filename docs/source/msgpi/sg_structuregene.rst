StructureGene
=============

.. currentmodule:: msgpi.sg

.. highlight:: python

::

    msgpi.sg.StructureGene


Constructor
-----------

.. autosummary::
    :toctree: sg/

    StructureGene









Attributes
----------

.. autosummary::
    :toctree: sg/

    StructureGene.name
    StructureGene.sgdim
    StructureGene.smdim
    StructureGene.analysis
    StructureGene.physics
    StructureGene.model
    StructureGene.trans_element
    StructureGene.nonuniform_temperature
    StructureGene.initial_curvature
    StructureGene.initial_twist
    StructureGene.oblique
    StructureGene.materials
    StructureGene.mocombos
    StructureGene.omega


Meshing data
^^^^^^^^^^^^

.. autosummary::
    :toctree: sg/

    StructureGene.nodes
    StructureGene.elements
    StructureGene.elementids
    StructureGene.elementids1d
    StructureGene.elementids2d
    StructureGene.elementids3d
    StructureGene.degen_element
    StructureGene.num_slavenodes
    StructureGene.elem_prop
    StructureGene.prop_elem


Dehomogenization data
^^^^^^^^^^^^^^^^^^^^^

.. autosummary::
    :toctree: sg/

    StructureGene.global_displacements
    StructureGene.global_rotations
    StructureGene.global_loads_type
    StructureGene.global_loads
    StructureGene.global_loads_dist









Methods
-------

.. autosummary::
    :toctree: sg/

    StructureGene.summary
    StructureGene.findMaterialByName
    StructureGene.findComboByMaterialOrientation


