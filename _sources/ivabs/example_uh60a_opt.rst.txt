Example 3: Optimization of UH60A with Dakota
--------------------------------------------

This example will use **Dakota** to explore the material choice, orientation angles, layers of the two webs and wing box of the UH60A airfoil to match the expected stiffness.

1. Get into ``ivabs-folder\examples\ex_uh60a_opt``
2. Open a command prompt.
3. (Optional) edit ``uh60a_opt_soga.in``. e.g. change ``evaluation_concurrency`` to add more cores to run it in parallel. The default value is 4.
4. Run ``dakota -i uh60a_opt_soga.in -o uh60a_opt_soga.out``
5. Read uh60a_opt_soga.out for the optimized design and error.

Among two laminas IM7 of 0.001 inch thickness and IM7 of 0.0008 inch thickness. The latter one is chosen. The optimized orientations angles of the 5 studied layers are

.. tabularcolumns:: |l|
.. table:: Optimized orientations of 5 studied layer
   :name: orient_layer
   :align: center

   +---------------------------------+
   |  :math:`\phantom{+}76.717123936`|
   +---------------------------------+
   |  :math:`-47.058626057`          |
   +---------------------------------+
   |  :math:`\phantom{+}4.0018921476`|
   +---------------------------------+
   |  :math:`-85.918454543`          |
   +---------------------------------+
   |  :math:`\phantom{+}34.209723197`|
   +---------------------------------+

Overall, the desired stiffness is reached within 2% error.

