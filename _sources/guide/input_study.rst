.. highlight:: yaml

.. _section-input_guide_study:

Design Study
============

This block specifies the actual study that is going to be carried out, e.g., parametric study or optimization.
iVABS inherits most of the keywords and layout of Dakota input.
Users can find more detailed guide from `Dakota's manual <https://dakota.sandia.gov/sites/default/files/docs/6.17.0-release/user-html/usingdakota/reference.html>`_.
Here only the differences are explained.
The overall layout is shown in :numref:`Listing %s <lst-input_study_layout>`.


..  code-block:: yaml
    :name: lst-input_study_layout
    :caption: Layout of the study input block

    study:
      method:
        ...
      variables:
        ...
      responses:
        ...
      interface:
        ...


Overall, same as Dakota, specifications are grouped into blocks.
The four important ones are method, variables, responses, and interface.









Method
---------

This blocks specifies the configurations for the study method.
The structure is the same as Dakota with the syntax as the only differece.
An example is given below comparing the different formats.

For example, to do 10 random sampling in the design space using the LHS method, the input using Dakota format is shown in :numref:`Listing %s <lst-input_study_method_dakota>` while the one using iVABS format is shown in :numref:`Listing %s <lst-input_study_method_ivabs>`.

..  code-block::
    :name: lst-input_study_method_dakota
    :caption: Dakota input for sampling

    method
      sampling
        sampling_type
          lhs
        samples = 10


..  code-block:: yaml
    :name: lst-input_study_method_ivabs
    :caption: iVABS input for sampling

    method:
      sampling:
        sample_type:
          lhs:
        samples: 10









Variables
------------

This block specifies the design variables used in the study.
The syntax of this block has the most difference from Dakota.
Instead of a hierarchical layout of keywords, iVABS uses a CSV style arrangement of inputs.
The general syntax is shown in :numref:`Listing %s <lst-input_study_variables>`.

..  code-block:: yaml
    :name: lst-input_study_variables
    :caption: Sample input for the variables block

    variables:
      data: |
        dv1, design, continuous, 0:1
        dv2, design, discrete, range, 1:9

All specifications of design variables are placed under the keyword ``data`` using the YAML literal block (:ref:`section-yaml_basic_scalars`).
Each row is a design variable entry starting by the *name*.
Specifications for a design variable includes *type*, *domain*, *space*, *class*, and other arguments.
*Name*, *type*, and *domain* are required for every design variable and the rest specifications depend on the choice of *domain*::

  <name>, <type>, <domain>, <args>

..  note::

    ``<>`` means a placeholder in this guide.
    It should be replaced with the actual keyword or argument in your input.

*Type* can be ``design`` or ``state``.
*Domain* can be ``continuous`` or ``discrete``.

If *domain* is ``continuous``, the last argument is the pair of numbers specifying the lower bound (``lb``) and upper bound (``ub``)::

  <name>, design, continous, <lb>:<ub>

If *domain* is ``discrete``, the next argument specifies the *space* of the design variable, which can be ``range`` or ``set``.
If *space* is ``range``, the last argument needed is the pair of of numbers specifying the lower and upper bounds::

  <name>, design, discrete, range, <lb>:<ub>

If *space* is ``set``, the next argument specifies the *class* of the design variable, which can be ``integer``, ``real``, or ``string``.
Then any number of values can follow *class*, specifying all options in the ``set``::

  <name>, design, discrete, set, <value1>, <value2>, <value3>, ...

Comments are indicated by a starting hash tag (``#``).
Commented lines are ignored by iVABS.

..  code-block:: yaml

    variables:
      data: |
        dv1, design, continuous, 0:1
        # dv2, design, discrete, range, 1:9









Responses
-----------

This block specifies the output needed in a design study, for instance simple responses for parametric studies and objectives and constraints for optimization.
Similar to the previous block for design variables, responses are also specified in a tabular list.
The general syntax is shown in :numref:`Listing %s <lst-input_study_responses>`.

..  code-block:: yaml
    :name: lst-input_study_responses
    :caption: Sample input for the responses block

    responses:
      data: |
        response1, objective, min, 0.5
        response2, objective, min, 0.8
        response3, inequality_constraint, 1:1e12

All specifications of responses are placed under the keyword ``data`` using the YAML literal block (:ref:`section-yaml_basic_scalars`).
Each row is a response entry starting by the *name*.
Specifications for a response includes *type* and other arguments.
*Name* and *type* are required for every response and the rest specifications depend on the choice of *type*::

  <name>, <type>, <args>

*Type* can be ``response``, ``objective`` or ``inequality_constraint``.

If *type* is ``response``, no more arguments needed::

  <name>, response

If *type* is ``objective``, the rest arguments specify the *sense* and *weight*::

  <name>, objective, <sense>, <weight>

*Sense* can be ``min`` or ``max``.
*Weight* is a number specifying the weighting factor for the current objective function.

If *type* is ``inequality_constraint``, the last argument is a pair of numbers specifying the lower bound (``lb``) and upper bound (``ub``)::

  <name>, inequality_constraint, <lb>:<ub>

Comments are indicated by a starting hash tag (``#``).
Commented lines are ignored by iVABS.

..  code-block:: yaml

    responses:
      data: |
        response1, objective, min, 0.5
        # response2, objective, min, 0.8
        response3, inequality_constraint, 1:1e12









Interface
-------------

Since iVABS is mainly integrated using Python, the analysis driver used by Dakota is "fork".
All configurations below this keyword are supported except ``link_files`` and ``copy_files`` which are used in Linux and Windows, respectively.
To simplify the input, a new keyword ``required_files`` is used to replace these two.

A typical example of this block is shown in :numref:`Listing %s <lst-input_study_interface>`


..  code-block:: yaml
    :name: lst-input_study_interface
    :caption: Sample input for the interface block

    interface:
      fork:
        parameters_file: "params.in"
        results_file: "results.out"
        file_save: on
        work_directory:
          directory_tag: on
          directory_save: on
      required_files:
        - "airfoil.dat"
        - "custom/*"
      asynchronous:
        evaluation_concurrency: 4
      failure_capture:
        recover: [-1, -1, -1]


