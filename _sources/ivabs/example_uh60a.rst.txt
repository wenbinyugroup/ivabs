Example 1: Automatic Process of Cross-sectional Analysis
========================================================


This example serves the purpose to demonstrate the workflow and scripting for running a cross-sectional analysis starting from passing in desgin parameters to extracting desired beam properties.
This process will be the core of design optimizations of composite slender structures.


Process setup
-------------

The cross-section input file template provides the overall design.
Among all parameters in the file, fiber angles of the four layers of the box spar are selected as those parameters requiring a separate input.

.. figure:: figures/ex_cs_analysis.png
  :name: fig_ex_cs_analysis
  :width: 6in
  :align: center


This process constains the following steps:

1. Assign/Get design parameters
2. Substitute parameter tokens in the template file with given values, and create the true cross-sectional input file
3. Run PreVABS and VABS for cross-sectional analysis
4. Get desired beam properties


This example contains the following files:

* ``process.py``: Process script
* ``uh60a_section.xml.tmp``: Cross-sectional design input template
* ``sc1095.dat``: Airfoil data
* ``material_database.xml``: Material database


Run
-----

1. Get into ``{IVABS_ROOT}\examples\ex_uh60a_cs_analysis_auto``.
2. Open a command prompt.
3. Run ``python process.py``.


Results
-------

If everything runs successfully, the prompt will print the following lines:

.. code-block::
  :linenos:

  INFO     | 2021-08-03 15:45:51 | process.process | start
  INFO     | 2021-08-03 15:45:51 | analysis.solve | preprocessing...
  INFO     | 2021-08-03 15:45:51 | presg.preSG | prevabs.exe -i uh60a_section.xml -vabs -h 
  INFO     | 2021-08-03 15:45:52 | analysis.solve | running analysis...
  INFO     | 2021-08-03 15:45:52 | analysis.runVABS | vabs uh60a_section.sg
  INFO     | 2021-08-03 15:45:54 | analysis.solve | reading results...
  INFO     | 2021-08-03 15:45:54 | process.process | finish
  EA = 42703405.884
  GJ = 19099828.485
  EI22 = 24152439.987
  EI33 = 841561460.1


Further reading
---------------

To understand more about how the cross-section is parameterized and how to prepare the design input file, please check :ref:`section-prevabs`.

To understand more about how to extract extract beam properties, please check :ref:`section-msgpi`.

.. The cross-section input file template provides the overall design.
.. Among all parameters in the file, fiber angles of the four layers of the box spar are selected as those parameters requiring a separate input (step 1).

.. .. code-block:: xml
..   :linenos:

..   <layup name="lyp_spar">
..     <layer lamina="T700 24K/E765_0.0056">{fa1}:10</layer>
..     <layer lamina="T700 24K/E765_0.0056">{fa2}:10</layer>
..     <layer lamina="T700 24K/E765_0.0056">{fa3}:10</layer>
..     <layer lamina="T700 24K/E765_0.0056">{fa4}:10</layer>
..   </layup>

.. Four numbers are assigned to the fiber angles in the process script.

.. .. code-block:: python
..   :linenos:

..   params = {
..       'fa1': 0,
..       'fa2': 90,
..       'fa3': 45,
..       'fa4': -45
..   }




.. .. figure:: figures/fig_uh60a_example.jpg
..   :name: fig_uh60a_example
..   :width: 5.5in
..   :align: center

.. This figure shows the construction model of PreVABS input. You should prepare 5 input files: basepoints.dat, baseline.xml, layup.xml, material.xml, section.xml. Current version of PreVABS also support combining all inputs in a single XML file.



.. The table below shows the 4x4 stiffness matrix for of classical beam model.

.. .. table:: Beam stiffness of UH60A airfoil
..    :name: uh60a_stiffness
..    :align: center

..    ============================= ============================= ============================= =============================
..    :math:`4.2369\times 10^{7}`   :math:`-8.1467\times 10^{3}`  :math:`4.6272\times 10^{5}`   :math:`-1.7006\times 10^{7}`
..    :math:`-8.1467\times 10^{3}`  :math:`1.6166\times 10^{5}`   :math:`-7.2404\times 10^{1}`  :math:`2.2351\times 10^{3}`
..    :math:`4.6272\times 10^{5}`   :math:`-7.2404\times 10^{1}`  :math:`1.4981\times 10^{5}`   :math:`-1.8577\times 10^{5}`
..    :math:`-1.7006\times 10^{7}`  :math:`2.2351\times 10^{3}`   :math:`-1.8577\times 10^{5}`  :math:`1.2608\times 10^{7}`
..    ============================= ============================= ============================= =============================

.. PreVABS features non-structural mass, ply drops, filler materials, building layups from sub-layups, and topology library.
