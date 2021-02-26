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
    :toctree: beam/

    BeamSegment


Attributes and underlying data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. autosummary::
    :toctree: beam/

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
    :toctree: beam/

    BeamSegment.calcLengthSq









Beam
----

Constructor
^^^^^^^^^^^

.. autosummary::
    :toctree: beam/

    Beam


Attributes and underlying data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. autosummary::
    :toctree: beam/

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
    :toctree: beam/

    Beam.echo
    Beam.findPtCoordByName
    Beam.findSectionByName
