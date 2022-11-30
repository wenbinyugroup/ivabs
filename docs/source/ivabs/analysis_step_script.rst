.. highlight:: python

.. _section-guide_analysis_script:


Custom Python Script for Analysis
===================================


What's the purpose of this?
---------------------------

The custom scripts provide users the flexibility to do calculations for special purposes that cannot be achieved using built-in functionalities in iVABS.
Typical usages of this include the pre- and post-processing of inputs and outputs of an analysis step.



How to prepare the custom scripts?
----------------------------------

The script file can be stored anywhere in the system.
There can be multiple functions in the file and they can be named arbitrarily.
However, there are some rules that users should follow when writing the functions so that they can be correctly called in the analysis workflow in iVABS.

..  note::

    These rules only apply to the functions that will be directly linked with iVABS.
    Users can still write functions freely if they are used only by other functions in the custom script, instead of iVABS.

The functions must have the following input list (names of the input variabels can be arbitrary):

..  code-block:: python

    def my_function(ivabs_data, structure_name, logger, *args, **kwargs):

        ...

From the first input variable to the last:

* ``ivabs_data``: The core data used by iVABS.
* ``structure_name``: The structure or cross-section name of the current analysis step.
* ``logger``: The logger object for generating logging information.
* ``*args``: Extra positional arguments provided by the user in the main input file.
* ``**kwargs``: Extra keyword arguments provided by the user in the main input file.


How to include the custom scripts in the main input file?
---------------------------------------------------------




Examples
--------

