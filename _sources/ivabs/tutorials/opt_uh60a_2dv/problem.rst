Problem Description
===================

The goal is to design the composite structure of a rotor blade to match some desired beam properties.

Scope of the study
------------------

This example assumes a uniform design along the span of the blade.
A specific topology which is a box spar design is considered for the structure, as shown in :numref:`Fig. %s <fig-cs_topo>`.
More details about the parameterization of the structure can be found in Section: :ref:`sect-cs-param`.

.. figure:: figures/cs_topo.png
    :name: fig-cs_topo
    :align: center

    Topology of the cross-section.

Specifications
--------------

Airfoil, chord length and target beam properties are summarized in :numref:`Table %s <tab-spec>`.

.. list-table:: Specifications
  :name: tab-spec
  :align: center
  :header-rows: 0

  * - Airfoil
    - SC1095
  * - Chord length
    - :math:`20.76\ \mathrm{in}`
  * - Mass per unit length (:math:`\hat{m}`)
    - :math:`0.00149\ \mathrm{lbf\cdot s^2 / in^2}`
  * - Torsional stiffness (:math:`\hat{GJ}`)
    - :math:`24.31\times 10^6\ \mathrm{lbf\cdot in^2}`
  * - Flapwise bending stiffness (:math:`\hat{EI}_f`)
    - :math:`22.20\times 10^6\ \mathrm{lbf\cdot in^2}`
  * - Lead-lag bending stiffness (:math:`\hat{EI}_l`)
    - :math:`835.00\times 10^6\ \mathrm{lbf\cdot in^2}`
  * - Horizontal location of the shear center from the leading edge (:math:`\hat{SC}_2^{le}`)
    - :math:`-5.19\ \mathrm{in}`
  * - Horizontal location of the mass center from the leading edge (:math:`\hat{MC}_2^{le}`)
    - :math:`-6.01\ \mathrm{in}`




