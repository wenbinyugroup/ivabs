A Simple Beam Class
===================

.. currentmodule:: msgpi.ms.beam

.. highlight:: python

::

    import msgpi.ms.beam

BeamSegment
------------

Constructor
^^^^^^^^^^^

.. autosummary::
    :toctree: _autogen/beam/
    :recursive:

    BeamSegment


Attributes and underlying data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. autosummary::
    :toctree: _autogen/beam/
    :recursive:

    BeamSegment.points
    BeamSegment.coords
    BeamSegment.css
    BeamSegment.rotate_a1
    BeamSegment.twist
    BeamSegment.local_frame_id
    BeamSegment.frame_id
    BeamSegment.curv_id
    BeamSegment.num_divisions


Methods
^^^^^^^

.. autosummary::
    :toctree: _autogen/beam/
    :recursive:

    BeamSegment.calcLengthSq









Beam
----

Constructor
^^^^^^^^^^^

.. autosummary::
    :toctree: _autogen/beam/
    :recursive:

    Beam


Attributes and underlying data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. autosummary::
    :toctree: _autogen/beam/
    :recursive:

    Beam.name
    Beam.analysis_type
    Beam.max_iteration
    Beam.num_steps
    Beam.num_eigens
    Beam.angular_velocity
    Beam.linear_velocity
    Beam.points
    Beam.segments
    Beam.pconditions
    Beam.mconditions
    Beam.sections
    Beam.frames
    Beam.distrloads
    Beam.timefunctions
    Beam.initcurvatures


Methods
^^^^^^^

.. autosummary::
    :toctree: _autogen/beam/
    :recursive:

    Beam.summary
    Beam.findPtCoordByName
    Beam.findSectionByName
    Beam.writeGmshMsh
    Beam.writeGEBTIn
