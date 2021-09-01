
.. _running:

Running of The Tutorial
=======================


To run the tutorial, use the following command:

.. code-block:: shell

  dakota -i cs_tm_opt_soga.dakota


If the optimization stops for some reason, to restart the optimization without doing everything from the beginning, use the following command:

.. code-block:: shell

  dakota -i cs_tm_opt_soga.dakota --read_restart cs_tm_opt_soga.rst


