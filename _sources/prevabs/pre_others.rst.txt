.. include:: replace.txt

.. _section-other:

Other components
----------------

Besides *Segment*\ s, user can use one material to fill a region. A typical usage is a nose mass in an airfoil type *Cross Section*. A schematic plot is shown in :numref:`Fig. %s <fig_filling1>`. In PreVABS, *Filling*\ s will be created after all *Segment*\ s are finished. Similar to a *Segment*, a *Filling* is defined by a *Baseline*, a *Material* (not *Layup*), and the filling side of the *Material*. The *Baseline* defines part of the boundaries of the region. The rest are found by the program automatically.

*Filling*\ s are also defined in the main input file. A template is shown in :numref:`Listing %s <code_fillings>`. All *Filling*\ s are placed in a single element ``<fillings>``. Each ``<filling>`` element has one attribute, ``name``, and two child elements, ``<baseline>`` and ``<material>``. The ``<material>`` element has an extra attribute, ``fillside``, which can only be ``left`` or ``right``. These have the same meaning as the ``direction`` attribute of a ``<layup>`` element in a ``<segment>`` definition.

.. note:: In the current version, *Filling* can only be used to create nose mass of an airfoil type *Cross Section*, and it is always filled to the left of the *Baseline*.

.. figure:: figures/filling1.png
  :name: fig_filling1
  :width: 6in
  :align: center

  Definition of a *Filling* as a nose mass in an airfoil type *Cross Section*.

.. code-block:: xml
  :linenos:
  :name: code_fillings
  :caption: A template for the *Filling*\ s in a main input file.

  <fillings>
    <filling name="filling1">
      <baseline>baseline1</baseline>
      <material fillside="left">material1</material>
    </filling>
    ...
  </fillings>



