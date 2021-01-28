.. include:: replace.txt

.. _section-recover:

Specifications for recovery
---------------------------

Once the 1D beam analysis is finished, those results can be used to recover local 3D strains and stresses at every point of the cross section. As stated in the VABS manual, the following data are required to carry out the recover analysis at a selected location along the beam:

- 1D beam displacements;
- rotations in the form of a direction cosine matrix;
- sectional forces and moments;
- distributed forces and moments, and their first three derivatives with respect to |x1|.

.. note:: The current version of PreVABS only performs recovery for Euler-Bernoulli model and Timoshenko model. If you want to perform recovery for other models such as the Vlasov model, please refer to the VABS manual to modify the input file yourself. 

These data are included in a ``<recover>`` element, added into the ``<cross_section>`` element in the main input file. The nine entries in the direction cosine matrix are flattened into a single array in the ``<rotations>`` element. This matrix is defined in Eq. :eq:`eq_direction_cosine`. Note that displacements and rotations are needed only for recovering 3D displacements. A template for this part of data is shown in :numref:`Listing %s <code_recover>`. Numbers in this template are defualt values. Once this file is updated correctly, the VABS recover analysis can be carried out as shown in :numref:`Section %s <section-command-option>`.

.. math::
  :label: eq_direction_cosine

  \mathbf{B}_i = C_{i1} \mathbf{b}_1 + C_{i2} \mathbf{b}_2 + C_{i3} \mathbf{b}_3 \quad \text{with} \quad i = 1, 2, 3

where :math:`\mathbf{B}_1`, :math:`\mathbf{B}_2`, and :math:`\mathbf{B}_3` are the base vectors of the deformed triad and :math:`\mathbf{b}_1`, :math:`\mathbf{b}_2`, and :math:`\mathbf{b}_3` are the base vectors of the undeformed triad.



.. code-block:: xml
  :linenos:
  :name: code_recover
  :caption: A template for the recover data in a *Cross section* file.

  <cross_section name="cs1" type="airfoil">
    ...
    <recover>
      <displacements>0 0 0</displacements>
      <rotations>1 0 0 0 1 0 0 0 1</rotations>
      <forces>0 0 0</forces>
      <moments>0 0 0</moments>
      <distributed>
        <forces>0 0 0</forces>
        <forces_d1>0 0 0</forces_d1>
        <forces_d2>0 0 0</forces_d2>
        <forces_d3>0 0 0</forces_d3>
        <moments>0 0 0</moments>
        <moments_d1>0 0 0</moments_d1>
        <moments_d2>0 0 0</moments_d2>
        <moments_d3>0 0 0</moments_d3>
      </distributed>
    </recover>
  </cross_section>


