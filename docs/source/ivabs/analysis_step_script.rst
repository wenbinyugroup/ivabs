.. highlight:: python

.. _section-guide_analysis_script:


Custom Python Script for Analysis
===================================


All functions should be defined in the following way to be correctly pluged in the analysis workflow in iVABS.


..  code-block:: python

    def my_function(ivabs_data, structure_name, logger, *args, **kwargs):

        ...

        return


