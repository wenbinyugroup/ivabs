.. _section-input_guide_design:

Design Parameters
=================

This block stores all information defining the structural design.
The overall layout is shown in :numref:`Listing %s <lst-input_design_layout>`.

..  code-block:: yaml
    :name: lst-input_design_layout
    :caption: Layout of the design input block

    design:
      - name: ""
        structure_class: ""
        parameters:
          list:
            ...
          distribution:
            ...
      - name: ""
        ...

Structures are arranged in a list/sequence.
Each one requires the specifications of name, class, and parameters.
Name (``name``) is a string that can be arbitrarily defined by the users.
Class (``structure_class``) specifies what type of structure this is.
Users choose one of built-in classes for this keyword.

..  note::
    Currently supported classes are blade (``blade``) and cross-section (``cs``).

..  note::
    Currently, only one ``blade`` class structure is supported.

Parameters (``parameters``) specify the values defining a specific design of the structure.
They can be given either in a list or as distributions with respect to the structural dimensions.
Supported parameters depend on the structural class.
For slender structures analyzed through cross-sections, please check the Section :ref:`section-ivabs_parameterization`.



Parameter specifications
--------------------------

List of parameters
^^^^^^^^^^^^^^^^^^^^^

In this section, structural design specifications are given in a list of pairs of parameter name and value.
The basic syntax is shown in :numref:`Listing %s <lst-input_design_param_list>`.

..  code-block:: yaml
    :name: lst-input_design_param_list
    :caption: Parameter list

    list:
      param_1: value_1
      param_2: value_2
      ...

Supported value types are number, string, and boolean.
Numbers can be integers or real numbers.
Strings should be put in double quotes (``"abc"``).
Booleans can be ``true``/``false``, ``yes``/``no``, or ``on``/``off``.

Parameter list can be used to specify a constant value for the whole structure.
These parameters can also be varied by an optimization method.
This is done by directly using the parameter name as the design variable name.




Distribution of parameters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In this section, structural parameters are defined as distribution functions with respect to the structural dimensions.
For slender structures that will be analyzed using beam models, this means that parameters are functions of a single coordinate along the longitudinal direction (e.g., blade span).
The basic syntax is shown in :numref:`Listing %s <lst-input_design_param_distr>`.


..  code-block:: yaml
    :name: lst-input_design_param_distr
    :caption: Parameter distribution

    distributions:
      - name: "..."
        function: "..."
        ...
      - name: "..."
        ...
      ...


Name (``name``) can be arbitrary for each distribution.
Function (``function``) is specified by choosing one of the built-in types such as interpolation functions.

..  note::
    Currently only interpolation function is supported.

Other specifications depend on the type of function selected.


Interpolation function
~~~~~~~~~~~~~~~~~~~~~~~



