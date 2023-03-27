.. _section-coordinate:

Coordinate systems
==================

There are three coordinate frames used in PreVABS as shown in
:numref:`Fig. %s <fig_frames>`:

- **z** is a basic frame, for the normalized airfoil data points for instance;
- **x** is the final frame;
- **y** is the local frame for each element.

.. figure:: /figures/frames.png
  :name: fig_frames
  :width: 6in
  :align: center

  The basic, cross-sectional and elementary frames in a cross section.

Here, |z1|, |x1| and |y1| are parallel to the tangent of the beam reference
line and pointing out of the paper. The basic frame is where base points
are defined. The cross-sectional and elementary frames have the same
definitions as those in VABS. User can define the topology of a cross
section in the basic frame **z** and use manipulations like translation,
scaling and rotation to generate the actual geometry in **x**. For an
airfoil cross section, airfoil surface data points downloaded from a
database having chord length 1 are in the frame **z**, and they are
transformed into the frame **x** through translation (re-define the
origin), scaling (multiplied by the actual chord length), and rotation
(attack angle) if necessary, as shown in :numref:`Fig. %s <fig_transforms>`.
More details about this transformation can be found in Section:
:ref:`section-overall` below.

.. figure:: /figures/transforms.png
  :name: fig_transforms
  :width: 100%
  :align: center

  Three manipulations to transform a cross section.

In PreVABS, the definition of the elementary frame **y** follows the
rule that the positive direction of |y2| axis is always the same as the
direction of the base line, and then |y3| is generated based on |y1|
and |y2| according to the right-hand rule. More details about the base
line can be found in :ref:`section-shape`.


