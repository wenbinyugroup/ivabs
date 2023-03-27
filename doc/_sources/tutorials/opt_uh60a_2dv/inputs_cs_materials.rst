
.. _sect-input-material:

Material Database (``material_database.xml``)
=============================================

The material database is a XML file. The format is 

.. code-block:: xml
  :linenos:

  <materials>
  <!--You can put arbitrary number of material tags-->
      <material name="[string]" type="<isotropic|orthotropic|lamina>">
          <density>[number]</density>
          <elastic>
          <!--For isotropic-->
              <e>[number]</e>
              <nu>[number]</nu>
          <!--For orthotropic-->
              <e1>[number]</e1>
              <e2>[number]</e2>
              <e3>[number]</e3>
              <g12>[number]</g12>
              <g13>[number]</g13>
              <g23>[number]</g23>
              <nu12>[number]</nu12>
              <nu13>[number]</nu13>
              <nu23>[number]</nu23>
          <!--For lamina or transverse isotropic-->
              <e1>[number]</e1>
              <e2>[number]</e2>
              <g12>[number]</g12>
              <nu12>[number]</nu12>
          </elastic>
      </material>
  <!--You can put arbitrary number of lamina tags-->
      <lamina name="[string]">
          <material>[string]</material>
          <thickness>[number]</thickness>
      </lamina>
  </materials> 

The unit system works like in Abaqus.
The user is responsible for keeping all the units consistent.
For other format specifications, you can refer to the actual material database file and comments.
Due to the file length, it's not included here.

For instance, Aluminum 8009 is used in the blade. The material property is :math:`E=13.1\times10^6\ \mathrm{psi}`,
:math:`\nu=0.33`. Therefore, it's declared in the database as

.. code-block:: xml
  :linenos:

  <material name="Aluminum 8009" type="isotropic">
      <!-- unit: lbf.sec^2/in^4 -->
      <density>0.271959e-3</density>
      <elastic>
          <!--unit:psi -->
          <e>13.1E+06</e>
          <nu>3.30E-01</nu>
      </elastic>
  </material>  

We also define the lamina used with the material and a thickness

.. code-block:: xml
  :linenos:

  <lamina name="Aluminum 8009_0.01">
      <material>Aluminum 8009</material>
      <thickness>0.01</thickness>
  </lamina>

The material definition is different for materials with different isotropy.
A commonly used group of materials is the lamina type material, which is 
transversely isotropic. Only the elastic terms in fiber direction are of
interest. For instance, the T650-35 12k/976 unidirectional tape's material
property is

.. csv-table:: T650-35 12k/976 Material Property (Psi)
  :name: t650
  :header-rows: 1
  :align: center

  :math:`E_1`, :math:`E_2`, :math:`G_{12}`, :math:`\nu_{12}`
  :math:`22\times 10^6`, :math:`1.3\times 10^6`, :math:`0.745\times 10^6`, :math:`0.115`

It's declaed as

.. code-block:: xml
  :linenos:

  <material name="T650-35 12k/976" type="lamina">
      <!-- unit: lbf.sec^2/in^4 -->
      <density>0.148781e-3</density>
      <elastic>
          <!-- unit: lbf/in^2 -->
          <e1>22.0E+06</e1>
          <e2>1.30E+06</e2>
          <g12>0.745E+06</g12>
          <nu12>1.150E-01</nu12>
      </elastic>
  </material>

The lamina definition is similar

.. code-block:: xml
  :linenos:

  <lamina name="T650-35 12k/976_0.0052">
      <material>T650-35 12k/976</material>
      <thickness>0.0052</thickness>
  </lamina>

Note that you can define multiple lamina types out of one material.
The lamina is a hierarchy in building the cross section. It's not the
aforementioned lamina type material, which just indicates the isotropy
of the material.


