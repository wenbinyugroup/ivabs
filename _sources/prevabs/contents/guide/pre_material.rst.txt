.. include:: /replace.txt

.. _section-material-layup:

Materials and layups
====================

PreVABS uses the keyword ``material`` for the physical properties attached to any materials, while ``lamina`` for material plus thickness, which in a sense is fixed by manufacturers.
This can be thought as the basic commercially available "material", such as a composite preprag.
A layer is a stack of laminae with the same fiber orientation.
The thickness of a layer can only be a multiplier of the lamina thickness.
Layup is several layers stacked together in a specific order.
This relationship is illustrated in :numref:`Fig. %s <fig_layup>`.
More details can be found below.

.. figure:: /figures/layup.png
  :name: fig_layup
  :width: 6in
  :align: center

  Relationship between material, lamina, layer and layup.

.. contents::









Material
---------

Both materials and laminae are stored in one XML file, under the single root element ``<materials>``.
A template of this file is shown in :numref:`Listing %s <code_material_temp>`.
Each material must have a name and type. Under each ``<material>`` element, there are a ``<density>`` element and an ``<elastic>`` element.
If failure analysis is wanted, users need to provide extra data including ``<strength>`` and ``<failure_criterion>``.

.. code-block:: xml
  :linenos:
  :name: code_material_layout
  :caption: Input syntax for materials.

  <materials>
    ...
    <material name="..." type="...">
      <density>...</density>
      <elastic>...</elastic>
      <strength>...</strength>
      <failure_criterion>...</failure_criterion>
    </material>
    ...
  </materials>

**Specification**

- **<material>** - Root element for each material.

  - *name* - Name of the material.
  - *type* - Type of the material. Choose one from 'isotropic', 'orthotropic', 'anisotropic' and 'lamina'.
  - **<density>** - Density of the material. Defualt is 1.0.
  - **<elastic>** - Elastic properties of the material. Specifications are different for different types.
  - **<strength>** - Strength properties of the material. Specifications are different for different types and different failure criterion.
  - **<failure_criterion>** - Failure criterion of the material. Options are different for different types.



Elastic properties
^^^^^^^^^^^^^^^^^^

.. code-block:: xml
  :linenos:
  :name: code_material_temp
  :caption: Input syntax for materials.

  <materials>
    ...
    <material name="iso1" type="isotropic">
      <elastic>
        <e>...</e>
        <nu>...</nu>
      </elastic>
    </material>

    <material name="lam1" type="lamina">
      <elastic>
        <e1>...</e1>
        <e2>...</e2>
        <nu12>...</nu12>
        <g12>...</g12>
      </elastic>
    </material>

    <material name="orth1" type="orthotropic">
      <elastic>
        <e1>...</e1>
        <e2>...</e2>
        <e3>...</e3>
        <g12>...</g12>
        <g13>...</g13>
        <g23>...</g23>
        <nu12>...</nu12>
        <nu13>...</nu13>
        <nu23>...</nu23>
      </elastic>
    </material>

    <material name="aniso1" type="anisotropic">
      <elastic>
        <c11>...</c11>
        <c12>...</c12>
        <c13>...</c13>
        <c14>...</c14>
        <c15>...</c15>
        <c16>...</c16>
        <c22>...</c22>
        <c23>...</c23>
        <c24>...</c24>
        <c25>...</c25>
        <c26>...</c26>
        <c33>...</c33>
        <c34>...</c34>
        <c35>...</c35>
        <c36>...</c36>
        <c44>...</c44>
        <c45>...</c45>
        <c46>...</c46>
        <c55>...</c55>
        <c56>...</c56>
        <c66>...</c66>
      </elastic>
    </material>
    ...
  </materials>


For the ``lamina`` type material, the code will internally convert it to the ``orthotropic`` type, by assigning the rest five constants in the following way:

- e3 = e2
- nu13 = nu12
- nu23 = 0.3
- g13 = g12
- g23 = e2 / ( 2 * (1 + nu23) )


**Specification**

- If *type="isotropic"* - 2 constants: 'e' and 'nu'.
- If *type="lamina"* - 4 constants: 'e1', 'e2', 'nu12' and 'g12'.
- If *type="orthotropic"* - 9 constants: 'e1', 'e2', 'e3', 'g12', 'g13', 'g23', 'nu12', 'nu13' and 'nu23'.
- If *type="anisotropic"* - 21 constants: 'c11', 'c12', 'c13', 'c14', 'c15', 'c16', 'c22', 'c23', 'c24', 'c25', 'c26', 'c33', 'c34', 'c35', 'c36', 'c44', 'c45', 'c46', 'c55', 'c56' and 'c66'. These constants are defined in Equation :eq:`hookeslaw`.
- If *type="lamina"* - 4 constants: 'e1', 'e2', 'g12' and 'nu12'. Internally, this type of material will be converted to the 'orthotropic' material. The default values for the rest components are: 'e3=e2', 'nu13=nu12', 'nu23=0.3', 'g13=g12' and 'g23=e3/(2*(1+nu23))'. These default values can be overwritten by custom values.

.. math::
  :label: hookeslaw

  \begin{Bmatrix}
    \sigma_{11} \\ \sigma_{12} \\ \sigma_{13} \\ \sigma_{22} \\ \sigma_{23} \\ \sigma_{33}
  \end{Bmatrix} =
  \begin{bmatrix}
    c_{11} & c_{12} & c_{13} & c_{14} & c_{15} & c_{16} \\
    c_{12} & c_{22} & c_{23} & c_{24} & c_{25} & c_{26} \\
    c_{13} & c_{23} & c_{33} & c_{34} & c_{35} & c_{36} \\
    c_{14} & c_{24} & c_{34} & c_{44} & c_{45} & c_{46} \\
    c_{15} & c_{25} & c_{35} & c_{45} & c_{55} & c_{56} \\
    c_{16} & c_{26} & c_{36} & c_{46} & c_{56} & c_{66}
  \end{bmatrix}
  \begin{Bmatrix}
    \epsilon_{11} \\ 2\epsilon_{12} \\ 2\epsilon_{13} \\ \epsilon_{22} \\ 2\epsilon_{23} \\ \epsilon_{33}
  \end{Bmatrix}


Strength properties
^^^^^^^^^^^^^^^^^^^

Inputs for strength properties for all types of materials have the same syntax.
For each material, users can input at least one or at most nine properties.
The overall syntax for each material is shown in :numref:`Listing %s <code_material_strength_overall>`.

.. code-block:: xml
  :linenos:
  :name: code_material_strength_overall
  :caption: Overall input syntax for strength properties.

  <material name="..." type="...">
    <failure_criterion>...</failure_criterion>
    <strength>
      <xt>...</xt>
      <yt>...</yt>
      <zt>...</zt>
      <xc>...</xc>
      <yc>...</yc>
      <zc>...</zc>
      <r>...</r>
      <t>...</t>
      <s>...</s>
    </strength>
  </material>

Although all properties will be stored internally, only some of them will be used in analysis depending on the failure criterion.

**Specification**

- **<xt>** - Tensile strength in |x1| direction. Alternative tags: <t1> or <x>. (Required)
- **<yt>** - Tensile strength in |x2| direction. Alternative tags: <t2> or <y>. (Optional. Default = <xt>.)
- **<zt>** - Tensile strength in |x3| direction. Alternative tags: <t3> or <z>. (Optional. Default = <yt>.)
- **<xc>** - Compressive strength in |x1| direction. Alternative tag: <c1>. (Optional. Default = <xt>.)
- **<yc>** - Compressive strength in |x2| direction. Alternative tag: <c2>. (Optional. Default = <yt>.)
- **<zc>** - Compressive strength in |x3| direction. Alternative tag: <c3>. (Optional. Default = <zt>.)
- **<s>** - Shear strength in |x1|-|x2| plane. Alternative tag: <s12>. (Required for specific failure criteria.)
- **<t>** - Shear strength in |x1|-|x3| plane. Alternative tag: <s13>. (Optional. Default = <s>)
- **<r>** - Shear strength in |x2|-|x3| plane. Alternative tag: <s23>. (Optional. Default = (<yt> + <yc>) / 4)


Failure criteria
^^^^^^^^^^^^^^^^

For isotropic materials, the following five failure criteria are available, followed by the strength constants needed:

1. **Max principal stress**. Strength constants (2):

  - 1 tensile strength (:math:`X`)
  - 1 compressive strength (:math:`X'`).

2. **Max principal strain**. Strength constants (2):

  - 1 tensile strength (:math:`X_{\varepsilon}`)
  - 1 compressive strength (:math:`X'_{\varepsilon}`).

3. **Max shear stress** or **Tresca**. Strength constant (1):

  - 1 shear strength (:math:`S`).

4. **Max shear strain**. Strength constant (1):

  - 1 shear strength (:math:`S_{\varepsilon}`)

5. **Mises**. Strength constant (1):

  - 1 strength (:math:`X`).

For other type materials (lamina, orthotropic, anisotropic), the following five failure criteria are available:

1. **Max stress**. Strength constants (9):

  - 3 tensile strengths in three directions (:math:`X, Y, Z`)
  - 3 compressive strengths in three directions (:math:`X', Y', Z'`)
  - 3 shear strengths in three principal planes (:math:`S, T, R`)

2. **Max strain**. Strength constants (9):

  - 3 tensile strengths in three directions (:math:`X_{\varepsilon}, Y_{\varepsilon}, Z_{\varepsilon}`)
  - 3 compressive strengths in three directions (:math:`X'_{\varepsilon}, Y'_{\varepsilon}, Z'_{\varepsilon}`)
  - 3 shear strengths in three principal planes (:math:`S_{\varepsilon}, T_{\varepsilon}, R_{\varepsilon}`)

3. **Tsai-Hill**. Strength constants (6):

  - 3 normal strengths in three directions (:math:`X, Y, Z`)
  - 3 shear shear strengths in three principal planes (:math:`S, T, R`).

4. **Tsai-Wu**. Strength constants (9):

  - 3 tensile strengths in three directions (:math:`X, Y, Z`)
  - 3 compressive strengths in three directions (:math:`X', Y', Z'`)
  - 3 shear strengths in three principal planes (:math:`S, T, R`)

5. **Hashin**. Strength constants (6):

  - 2 tensile strengths in two directions (:math:`X, Y`)
  - 2 compressive strengths in two directions (:math:`X', Y'`)
  - 2 shear strengths in two principal planes (:math:`S, R`)

Different failure criterion will use different strength properties.
This is summarized in the table below.

.. csv-table:: Strength properties used by different failure criteria.
  :header-rows: 1
  :align: center

  Failure criterion,x/xt/t1,y/yt/t2,z/zt/t3,xc/c1,yc/c2,zc/c3,s/s12,t/s13,r/s23
  **Isotropic**
  Max principal stress, :math:`X`,,, :math:`X'`,,, ,,
  Max principal strain, :math:`X_{\varepsilon}`,,, :math:`X'_{\varepsilon}`,,, ,,
  Max shear stress, ,,, ,,, :math:`S`,,
  Max shear strain, ,,, ,,, :math:`S_{\varepsilon}`,,
  Mises, :math:`X`,,, ,,, ,,
  **Not isotropic**
  Max stress,  :math:`X`, :math:`Y`, :math:`Z`,  :math:`X'`, :math:`Y'`, :math:`Z'`,  :math:`S`, :math:`T`, :math:`R`
  Max strain,  :math:`X_{\varepsilon}`, :math:`Y_{\varepsilon}`, :math:`Z_{\varepsilon}`,  :math:`X'_{\varepsilon}`, :math:`Y'_{\varepsilon}`, :math:`Z'_{\varepsilon}`,  :math:`S_{\varepsilon}`, :math:`T_{\varepsilon}`, :math:`R_{\varepsilon}`
  Tsai-Hill, :math:`X`, :math:`Y`, :math:`Z`, ,,, :math:`S`, :math:`T`, :math:`R`
  Tsai-Wu,  :math:`X`, :math:`Y`, :math:`Z`,  :math:`X'`, :math:`Y'`, :math:`Z'`,  :math:`S`, :math:`T`, :math:`R`
  Hashin, :math:`X`, :math:`Y`,, :math:`X'`, :math:`Y'`,, :math:`S`,, :math:`R`


More details can be found in the VABS users manual [VABS]_.

**Specification**

- **<failure_criterion>** - Name or ID of the failure criterion used.

  - If *type="isotropic"*, choose one of the following:

    - ``1`` or ``max principal stress``
    - ``2`` or ``max principal strain``
    - ``3`` or ``max shear stress`` or ``tresca``
    - ``4`` or ``max shear strain``
    - ``5`` or ``mises``

  - If *type="lamina"* or *type="orthotropic"* or *type="anisotropic"*, choose one of the following:

    - ``1`` or ``max stress``
    - ``2`` or ``max strain``
    - ``3`` or ``tsai-hill``
    - ``4`` or ``tsai-wu``
    - ``5`` or ``hashin``









Lamina
------

Each lamina element has a name, and contains a material name and a value for thickness.
The input syntax is shown in :numref:`Listing %s <code_lamina_temp>`.

.. code-block:: xml
  :linenos:
  :name: code_lamina_temp
  :caption: Input syntax for lamina.

  <materials>
    ...
    <lamina name="lamina1">
      <material> orth1 </material>
      <thickness>...</thickness>
    </lamina>
    ...
  </materials>

**Specification**

- **<lamina>** - Root element for the definition of each lamina.

   - *name* - Name of the lamina.

- **<material>** - Name of the material of the lamina.
- **<thickness>** - Thickness of the lamina.










Layups
------

In general, there are two ways to define a layup, explicit list and stacking sequence code.
For the explicit list, a laminate is laid onto the base line from the first layer in the list to the last one, in the direction given by the user.
For the stacking sequence, the layup starts from left to the right.
User should pay attention to the relations among the base line direction, elemental frame **y** and fiber orientation :math:`\theta_3` of each layer, as shown in :numref:`Fig. %s <fig_elementalframe>`.
Change of direction of the base line will change the elemental frame **y** as defined, which will further require the user to change the fiber orientations accordingly, even though nothing changes physically.
All layup information are included in one XML file.
A template of this file can be found in :numref:`Listing %s <code_layup_temp>`.

.. figure:: /figures/elementalframe.png
  :name: fig_elementalframe
  :width: 6in
  :align: center

  Relations among the base line direction, elemental frame **y** and fiber orientation (Note $y_2$ is parallel to the base line direction).

.. code-block:: xml
  :linenos:
  :name: code_layup_temp
  :caption: Input syntax for layups.

  <layups>
    <layup name="layup1" method="explicit list">
      <layer lamina="lamina1">...</layer>
      ...
    </layup>
    <layup name="layup2" method="stack sequence">...</layup>
    <layup name="layup3" method="ply percentage">...</layup>
    ...
  </layups>

**Specification**

- **<layup>** - Root element for the definition of each layup.

  - *name* - Name of the layup.
  - *method* - Method of defining the layup. Choose one from 'layer list' (or 'll') and 'stack sequence' (or 'ss'). Default is 'layer list'.




Explicit list
^^^^^^^^^^^^^

This method requires user to write down the lamina name, fiber orientation
and number of successive laminas with the same fiber orientation, layer
by layer. Alternatively, a layer can also be defined by the name of a sublayup.
A sublayup must appear before the layup where it is referenced.
A template for one layer is shown below.

.. code-block:: xml
  :linenos:
  :name: code_layup_ll_temp
  :caption: A template for the layup layer list input.

  <layups>
    ...
    <layup name="...">
      <layer lamina="lamina_name"> angle:stack </layer>
      <layer lamina="lamina_name"> angle:stack </layer>
      <layer lamina="lamina_name"> angle:stack </layer>
      <layer layup="sublayup_name"/>
      ...
    </layup>
    ...
  </layups>

**Specification**

- **<layer>** - Material orientation and number of plies separated by a colon 'angle:stack'. Default values are 0 for 'angle' and 1 for 'stack'. If there is only one number presented in this element, then it is read in as 'angle', not 'stack', which is 1 by default.

  - *lamina* - Optional. Name of the lamina used in the current layer.
  - *layup* - Optional. Name of the sublayup used in the current layer. One and only one of *lamina* and *layup* should be used. 'angle' and 'stack' are not needed when *layup* is used.

An example for the layup shown in :numref:`Fig. %s <fig_layup>` is given
in :numref:`Listing %s <code_material>` and :numref:`Listing %s <code_layup>`.





Stacking sequence code
^^^^^^^^^^^^^^^^^^^^^^

This method requires users to provide one lamina name and the stacking
sequence code. A template is shown below.

.. code-block:: xml
  :linenos:
  :name: code_layup_ss_temp
  :caption: A template for the layup stacking sequence input.

  <layups>
    ...
    <layup name="..." method="stack sequence">
      <lamina>...</lamina>
      <code>...</code>
    </layup>
    ...
  </layups>

**Specification**

- **<lamina>** - Name of the lamina used.
- **<code>** - Stacking sequency code. Explained below.

**Rules of writing the stacking sequence code**

- All fiber orientations should be put between a pair of square brackets ``[]``;
- Different fiber orientations are separated by slash ``/``;
- After the right bracket, user can add ``ns`` to indicate symmetry of the layup, where ``n`` is the number of the symmetry operations needed to generate the complete layup;
- Successive laminae with the same fiber orientation can be expressed using colon like ``angle:stack``, where ``angle`` is the fiber orientation and ``stack`` is the number of plies;
- If a group of fiber orientations is repeated, user needs to close them in a pair of round brackets ``()``.

Examples

.. csv-table:: Examples of stacking sequence code
  :header-rows: 1
  :align: center

  Code, Complete sequence
  ``[0/90]2s``, "0, 90, 90, 0, 0, 90, 90, 0"
  ``[(45/-45):2/0:2]s``, "45, -45, 45, -45, 0, 0, 0, 0, -45, 45, -45, 45"

.. Ply/Lamina percentage code
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~

.. (Will be available in a future version)

.. code-block:: xml
  :linenos:
  :name: code_material
  :caption: Example material and lamina input file for the layup shown in :numref:`Fig. %s <fig_layup>`.

  <materials>
    <material name="square" type="orthotropic">
      <density>...</density>
      <elastic>...</elastic>
    </material>

    <material name="hexagon" type="orthotropic">
      <density>...</density>
      <elastic>...</elastic>
    </material>

    <lamina name="la_square_15">
      <material> square </material>
      <thickness> 1.5 </thickness>
    </lamina>

    <lamina name="la_hexagon_10">
      <material> hexagon </material>
      <thickness> 1.0 </thickness>
    </lamina>
  </materials>

.. code-block:: xml
  :linenos:
  :name: code_layup
  :caption: Example layup input file for the layup shown in :numref:`Fig. %s <fig_layup>`.

  <layups>
    <layup name="layup_el" method="explicit list">
      <layer lamina="la_hexagon_10"> 45:2 </layer>
      <layer lamina="la_hexagon_10"> 90 </layer>
      <layer lamina="la_square_15"></layer>
      <layer lamina="la_hexagon_10"> -45:2 </layer>
      <layer lamina="la_square_15"> 0:2 </layer>
      <layer lamina="la_hexagon_10"> -45:2 </layer>
      <layer lamina="la_square_15"></layer>
      <layer lamina="la_hexagon_10"> 90 </layer>
      <layer lamina="la_hexagon_10"> 45:2 </layer>
    </layup>

    <layup name="layup_ss" method="stack sequence">
      <lamina> la_square_15 </lamina>
      <code> [(45/-45):2/0:4/90]2s </code>
    </layup>
  </layups>


