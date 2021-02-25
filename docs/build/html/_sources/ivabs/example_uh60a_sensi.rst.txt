Example 2: Sensitivity analysis of UH60A with Dakota
----------------------------------------------------

.. figure:: figures/fig_uh60a_example_sensi.jpg
  :name: fig_uh60a_example_sensi
  :width: 5.5in
  :align: center

This example will use **Dakota** to conduct a sensitivity analysis to find out the most important design parameters. The studied airfoil is UH60A. The studied design parameters are fiber orientations and number of plies of box spar, webs. See the design template file ``uh60a_layup.xml.tmp`` for details. The method used is ``Design and Analysis of Computer Experiments(dace)`` package of **Dakota**. variance-based decomposition is used as the sensitivity measure. See **Dakota** documentation for details.

1. Get into ``ivab-folder\examples\ex_uh60a_sensi``;
2. Open a command prompt;
3. (Optional) edit ``uh60a_dace.in``. e.g. change ``evaluation_concurrency`` to add more cores to run it in parallel. The default value is 4;
4. Run ``dakota -i uh60a_dace.in -o uh60a_dace.out``;
5. Read ``uh60a_dace.out`` for the sensitivity analysis result.

As a summary, the box spar fiber orientation is the most important design parameter.
