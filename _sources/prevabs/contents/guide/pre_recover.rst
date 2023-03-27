.. _section-recover:

Specifications for recovery
===========================

VABS
----

Once the 1D beam analysis is finished, those results can be used to
recover local 3D strains and stresses at every point of the cross section.
As stated in the VABS manual, the following data are required to carry
out the recover analysis at a selected location along the beam:

- 1D beam displacements;
- rotations in the form of a direction cosine matrix;
- sectional forces and moments;
- distributed forces and moments, and their first three derivatives with
  respect to |x1|.

.. note:: The current version of PreVABS only performs recovery for
  Euler-Bernoulli model and Timoshenko model. If you want to perform
  recovery for other models such as the Vlasov model, please refer to
  the VABS manual to modify the input file yourself.

These data are included in a ``<global>`` element, added into the
``<cross_section>`` element in the main input file. The nine entries
in the direction cosine matrix are flattened into a single array in the
``<rotations>`` element. This matrix is defined in
Eq. :eq:`eq_direction_cosine`. Note that displacements and rotations
are needed only for recovering 3D displacements. A template for this
part of data is shown in :numref:`Listing %s <code_recover>`. Numbers
in this template are defualt values. Once this file is updated correctly,
the VABS recover analysis can be carried out as shown in Section:
:ref:`section-command-option`.

.. math::
  :label: eq_direction_cosine

  \mathbf{B}_i = C_{i1} \mathbf{b}_1 + C_{i2} \mathbf{b}_2 + C_{i3} \mathbf{b}_3 \quad \text{with} \quad i = 1, 2, 3

where :math:`\mathbf{B}_1`, :math:`\mathbf{B}_2`, and :math:`\mathbf{B}_3`
are the base vectors of the deformed triad and :math:`\mathbf{b}_1`,
:math:`\mathbf{b}_2`, and :math:`\mathbf{b}_3` are the base vectors of
the undeformed triad.

.. code-block:: xml
  :linenos:
  :name: code_recover
  :caption: A template for the recover data in a *Cross section* file.

  <cross_section name="cs1">
    ...
    <dehomo> 1 </dehomo>
    <global>
      <displacements> 0 0 0 </displacements>
      <rotations> 1 0 0 0 1 0 0 0 1 </rotations>
      <loads> 0 0 0 0 0 0 </loads>
      <distributed>
        <forces> 0 0 0 </forces>
        <forces_d1> 0 0 0 </forces_d1>
        <forces_d2> 0 0 0 </forces_d2>
        <forces_d3> 0 0 0 </forces_d3>
        <moments> 0 0 0 </moments>
        <moments_d1> 0 0 0 </moments_d1>
        <moments_d2> 0 0 0 </moments_d2>
        <moments_d3> 0 0 0 </moments_d3>
      </distributed>
    </global>
  </cross_section>

**Specification**

- **<global>** - Global analysis results. Required.
- **<displacements>** - Three components (|u1|, |u2|, |u3|) of the global displacements. Optional. Default values are {0, 0, 0}.
- **<rotations>** - Nine components (|c11|, |c12|, |c13|, |c21|, |c22|, |c23|, |c31|, |c32|, |c33|) of the global rotations (direction cosine matrix). Optional. Default values are {1, 0, 0, 0, 1, 0, 0, 0, 1}.
- **<loads>** - The sectional loading components. For the Euler-Bernoulli model, four numbers (|F1|, |M1|, |M2|, |M3|) are needed. For the Timoshenko model, six numbers (|F1|, |F2|, |F3|, |M1|, |M2|, |M3|) are needed. Optional. Default values are zero loads.
- **<distributed>** - Distributed sectional loads per unit span (Timoshenko model only). Optional. Default values are zero distributed loads.

  - **<forces>** - Distributed sectional forces (|f1|, |f2|, |f3|).
  - **<forces_d1>** - First derivative of distributed sectional forces (|f'1|, |f'2|, |f'3|).
  - **<forces_d2>** - Second derivative of distributed sectional forces (|f''1|, |f''2|, |f''3|).
  - **<forces_d3>** - Third derivative of distributed sectional forces (|f'''1|, |f'''2|, |f'''3|).
  - **<moments>** - Distributed sectional moments (|m1|, |m2|, |m3|).
  - **<moments_d1>** - First derivative of distributed sectional moments (|m'1|, |m'2|, |m'3|).
  - **<moments_d2>** - Second derivative of distributed sectional moments (|m''1|, |m''2|, |m''3|).
  - **<moments_d3>** - Third derivative of distributed sectional moments (|m'''1|, |m'''2|, |m'''3|).

- **<dehomo>** - Order of theory for dehomogenization, 1 for nonlinear beam theory and 2 for linear beam theory. Optional. Default is 2.









SwiftComp
---------

.. code-block:: xml
  :linenos:
  :name: code_dehomo_sc
  :caption: Syntax for the dehomogenization inputs for SwiftComp.

  <global measure="stress">
    <displacements> 0 0 0 </displacements>
    <rotations> 1 0 0 0 1 0 0 0 1 </rotations>
    <loads> 0 0 0 0 0 0 </loads>
  </global>

**Specification**

- **<global>** - Global analysis results. Required.

  - *measure* - Type of the sectional loads, ``stress`` for generalized stresses and ``strain`` for generalized strains. Required.

- **<displacements>** - Three components (|u1|, |u2|, |u3|) of the global displacements. Optional. Default values are {0, 0, 0}.
- **<rotations>** - Nine components (|c11|, |c12|, |c13|, |c21|, |c22|, |c23|, |c31|, |c32|, |c33|) of the global rotations (direction cosine matrix). Optional. Default values are {1, 0, 0, 0, 1, 0, 0, 0, 1}.
- **<loads>** - The sectional loading components. For the Euler-Bernoulli model, four numbers (|F1|, |M1|, |M2|, |M3|) are needed. For the Timoshenko model, six numbers (|F1|, |F2|, |F3|, |M1|, |M2|, |M3|) are needed. Optional. Default values are zero loads.

