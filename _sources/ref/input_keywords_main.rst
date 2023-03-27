.. _section-ref_input_keywords:

Main Input Keywords
===================

Setting (``setting``)
----------------------


``log_level_cmd``
^^^^^^^^^^^^^^^^^^^

Set the level of logging messages printed to the command line.

* **Optional**
* **Type**: String
* **Arguments**: debug\|info\|warning\|error\|critical
* **Default**: info

Use the default Python logging levels (case insensitive).
``debug`` prints the most information, while ``critical`` prints the least.


``log_level_file``
^^^^^^^^^^^^^^^^^^^^^

Set the level of logging messages printed to the log file.

* **Optional**
* **Type**: String
* **Arguments**: debug\|info\|warning\|error\|critical
* **Default**: info

Use the default Python logging levels (case insensitive).
``debug`` prints the most information, while ``critical`` prints the least.


``log_file_name``
^^^^^^^^^^^^^^^^^^^^

Set the name of the log file.

* **Optional**
* **Type**: String
* **Arguments**: Any valid file name
* **Default**: log.txt


..  literalinclude:: /files/main_input_ref.yml
    :caption: Example
    :language: yaml
    :start-after: [setting]
    :end-before: [structure]
    :linenos:









Structure (``structure``)
----------------------------

``name``
^^^^^^^^^^

Name of the structure.
Used only in logging messages.

* **Optional**
* **Type**: String
* **Arguments**: Arbitrary
* **Default**: structure_0


``parameter``
^^^^^^^^^^^^^^^

Key-value pairs of the design parameters for the whole structure.

* **Optional**
* **Type**: Dictionary
* **Arguments**: ``key: value`` pairs
* **Default**: None

..  code-block:: yaml
    :caption: Example
    :linenos:

    structure:
      parameter:
        param1: "value1"
        param2: 2
        param3: 3.0
        param4: 4e5
        param5: true  # or on
        param6: false  # or off

``design``
^^^^^^^^^^^^

Basic design setup of the structure.

* **Optional**
* **Type**: Dictionary



..  literalinclude:: /files/main_input_ref.yml
    :caption: Example
    :language: yaml
    :start-after: [structure]
    :end-before: [sg]
    :linenos:









Cross-section library (``cs``)
--------------------------------

This block contains a list of cross-sectional base designs.

..  code-block:: yaml
    :caption: Example
    :linenos:

    cs:
      - name: "cs_base_design_1"
        ...
      - name: "cs_base_design_2"
        ...

``name``
^^^^^^^^^^

Name of the cross-sectional base design.

* **Required**
* **Type**: String
* **Arguments**: Arbitrary
* **Default**: None

``parameter``
^^^^^^^^^^^^^^^

Key-value pairs of the design parameters for the current CS.

* **Optional**
* **Type**: Dictionary
* **Arguments**: ``key: value`` pairs
* **Default**: None

``design``
^^^^^^^^^^^^

Basic design setup of the current CS.

* **Optional**
* **Type**: Dictionary

``tool``
^^^^^^^^^^

PreVABS command used to create the cross-section.

* **Optional**
* **Type**: String
* **Default**: prevabs

``base_file``
^^^^^^^^^^^^^^

File name of the cross-sectional design template.

* **Required**
* **Type**: String
* **Default**: None




..  literalinclude:: /files/main_input_ref.yml
    :caption: Example
    :language: yaml
    :start-after: [sg]
    :end-before: [analysis]
    :linenos:









Analysis (``analysis``)
-------------------------

..  code-block:: yaml
    :caption: Example
    :linenos:

    analysis:
      steps:
        - step: "step 1"
          type: "cs"
          ...
        - step: "step 2"
          ...


``steps``
^^^^^^^^^^

Specification of analysis steps.

* **Required** (at least one step)
* **Type**: List
* **Default**: None


``step``
^^^^^^^^^^

Name of the current step.

* **Required**
* **Type**: String

``type``
^^^^^^^^^^

Type of the current analysis step.

* **Required**
* **Type**: String
* **Arguments**: cs\|script

``cs`` defines a cross-sectional analysis step.
``script`` defines a custom step using user-provided Python scripts.

Related pages

* :ref:`section-guide_analysis_script`

``analysis``
^^^^^^^^^^^^^^

Use under::

    analysis:
      steps:
        - step: "..."
          type: "cs"
          analysis: "..."

Specify the cross-sectional analysis type.

* **Required**
* **Type**: String
* **Arguments**: h\|fi

``file``
^^^^^^^^^^^^

Use under::

    analysis:
      steps:
        - step: "..."
          type: "script"
          file: "..."

Name of the custom Python script file.

* **Required**
* **Type**: String

Related pages

* :ref:`section-guide_analysis_script`

``function``
^^^^^^^^^^^^^^

Use under::

    analysis:
      steps:
        - step: "..."
          type: "script"
          function: "..."

Name of the custom Python function.

* **Required**
* **Type**: String

Related pages

* :ref:`section-guide_analysis_script`

``args``
^^^^^^^^^^^^

Use under::

    analysis:
      steps:
        - step: "..."
          type: "script"
          args:
            - arg1
            - arg2
            - ...

Extra positional arguments passed to the custom Python function.

* **Optional**
* **Type**: List

Related pages

* :ref:`section-guide_analysis_script`

``kwargs``
^^^^^^^^^^^^

Use under::

    analysis:
      steps:
        - step: "..."
          type: "script"
          kwargs:
            kw1: arg1
            kw2: arg2
            ...

Extra keyword arguments passed to the custom Python function.

* **Optional**
* **Type**: Dictionary

Related pages

* :ref:`section-guide_analysis_script`

..  literalinclude:: /files/main_input_ref.yml
    :caption: Example
    :language: yaml
    :start-after: [analysis]
    :end-before: [study]
    :linenos:









Design study configuration (``study``)
-------------------------------------------

Most of the keywords in this block are the same as those of Dakota.
See their `documentation <https://dakota.sandia.gov/sites/default/files/docs/6.17.0-release/user-html/usingdakota/reference.html>`_ for more information.

Related pages:

* :ref:`section-input_guide_study`

..  literalinclude:: /files/main_input_ref.yml
    :caption: Example
    :language: yaml
    :start-after: [study]
    :end-before: [end]
    :linenos:


