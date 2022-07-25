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

This option (``function: "interpolation"``) creates one or multiple distribution functions by interpolating a table of data.


..  code-block:: yaml
    :name: lst-input_design_param_distr_interp
    :caption: Interpolation function

    distributions:
      - name: "..."
        function: "interpolation"
        kind: "linear"
        xnames: "x"
        ynames: ["a", "b", "c"]
        ytypes: ["float", "int", "string"]
        data: |
          x1, a1, b1, c1
          x2, a2, b2, c2
          ...


This function supports two different kinds, indicated by the keyword ``kind``: linear (``linear``) and previous (``previous``).
Suppose we want to get the value y at x which locates between x1 and x2.
Given two data (x1, y1) and (x2, y2), ``linear`` kind function means that y is calculated by linearly interpolating these two data.
``previous`` kind function uses the value at the location no greater than x (y=y1 in this case).

The set of data is specified by multiple keywords.
``xnames`` and ``ynames`` are used to specify the list of names or labels of the independent and dependent variables, respectively.
Generally, labels should be placed in square brackets, delimited by commas.
If there is only one label, the square brackets can be omitted.
Currently iVABS only create scalar functions with a single output.
Hence, the labels in ``ynames`` indicates all the functions that will be created.

``data`` is used to place the actual data that will be interpolated.
This is a literal block indicated by the vertical bar (see Section :ref:`section-yaml_basic_scalars`).
Values are arranged in a tabular form.
Each row is an entry of the data and values are separated by commas.
If ``kind`` is ``linear``, there should be as least two entries.
If ``kind`` is ``previous``, a single entry is acceptable.
Each column is either an independent or dependent variable.
In the most general case, the first :math:`n` columns correspond to the :math:`n` ``xnames``.
Then the next :math:`m` columns correspond to the :math:`m` ``ynames``.
Hence, the number of columns should be the same as the number of labels in both ``xnames`` and ``ynames``.

Different types of values can be specified using the keyword ``ytypes``.
By default, all values are treated as real numbers (``float``).
Other supported types are integer numbers (``int``) and strings (``string``).
Different parameters (``ynames``) can have the same or different types.
If ``ytypes`` is a string, then the type will be applied to all parameters listed in ``ynames``.
Otherwise, ``ytypes`` must have the same size as ``ynames``.

All quantities in the data block can be marked as design variables that will be changed later by Dakota.
The design variable name is prepended to the value followed by a colon:

..  code-block:: yaml

    ynames: ["a", "b", "c"]
    data: |
      x1, dv2: a1, dv3: b1, c1
      dv1: x2, a2, dv4: b2, c2
      ...

In this case, "dv1" to "dv4" are four design variables used by Dakota.
During any iterative process (parametric study, optimization, etc.), values marked by the design variable names will be substituted by new values generated in the current iteration.
It is acceptable that a quantity is marked by a label but not used in Dakota.
In other words, values after the colon can be treated as the default ones.
