.. highlight:: yaml

.. _section-yaml:

A Brief Introduction to YAML
====================================

There are many features and functionalities of YAML.
iVABS only use the most basic ones.
More about YAML can be found from:

* https://yaml.org/spec/1.2.2/#chapter-2-language-overview
* https://www.tutorialspoint.com/yaml/yaml_basics.htm



.. _section-yaml_basic:

Basic syntax
--------------


.. _section-yaml_basic_collections:

Collections and structures
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Mappings use a colon and space (``:``) to mark each key/value pair:

..  code-block:: yaml

    key1: value1
    key2: value2

Supported value types are number, string, and boolean.
Numbers can be integers or real numbers.
Strings should be put in double quotes (``"abc"``).
Booleans can be ``true``/``false``, ``yes``/``no``, or ``on``/``off``.

Sequences indicate each entry with a dash and space (``-``):

..  code-block:: yaml

    - value1
    - value2

Sequences can also be indicated using square brackets and commas:

..  code-block:: yaml

    [value1, value2, ...]


Indentation of whitespace is used to denote structure.

..  code-block:: yaml

    key:
      subkey1:
        subsubkey: subsubvalue
      subkey2: subvalue


Mappings and sequences can be mixed.

..  code-block:: yaml

    key:
      - value1
      - value2
      - subkey: [subvalue1, subvalue2, ...]


Comments begin with a hash tag (``#``).

..  code-block:: yaml

    # A line of coment.


.. _section-yaml_basic_scalars:

Scalars
^^^^^^^^^


Literal blocks are indicated by a vertical bar (``|``):

..  code-block:: yaml

    key: |
      Any characters can be placed here.
      Line breaks will be preserved.




