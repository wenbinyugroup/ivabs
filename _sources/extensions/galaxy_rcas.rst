.. highlight:: python

.. _section-extensions-galaxy_rcas:

Link to Galaxy/RCAS
====================

All functions below are in the module ``msgd.ms.rcas``.


Read the OML data (``readRcasOml``)
-------------------------------------

..  code-block:: python

    import msgd.ms.rcas as mmr
    oml = mmr.readRcasOml('oml.dat')

Returned value of this function is a Python dictionary having the following data layout.

..  code-block:: python

    oml = {
        'fenode': fe_nodes,
        'aeronode': aero_nodes,
        'aeroseg': aero_segs,
        'airfoilinterp': airfoil_interp
    }

``oml['fenode']``
    Data block "FENODE".
    A dictionary of structural nodal ID and coordinates: ``{id1: [x1, y1, z1], id2: [x2, y2, z2], ...}``.

``oml['aeronode']``
    Data block "AERONODE".
    A dictionary of aerodynamic nodal ID and coordinates: ``{id1: [x1, y1, z1], id2: [x2, y2, z2], ...}``.

``oml['aeroseg']``
    Data block "AEROSEG".
    A dictionary of aerodynamic segments.

    ..  code-block:: python

        {
            seg1_id: {
                'aero_nodes': [pnode_id, cnode_id],
                'chord': c,
                'airfoil': 'airfoil_name',
                'twist': t,
                'shear': s
            },
            seg2_id: {...},
            ...
        }

``oml['airfoilinterp']``
    Data block "AIRFOILINTERP".
    A dictionary of radial location and airfoil name: ``{'r': [r1, r2, ...], 'airfoil': ['name1', 'name2', ...]}``.









Read the property data (``readRcasProp``)
------------------------------------------

..  code-block:: python

    import msgd.ms.rcas as mmr
    prop = mmr.readRcasProp('prop.dat')

Returned value of this function is a Python dictionary having the following data layout.

..  code-block:: python

    prop = {
        'prop1_name': value,
        'prop2_name': {'x': [], 'y': []},
        'prop3_name': [],
        ...
    }

Each key in this dictionary is the property name in the file (without the leading "!M " characters), such as "BEA", "BGJ", etc.
For the values, there are three types:

**Scalar** (``prop['prop1_name']``).
There is only a single value corresponding to the property, such as 'REFLENGTH'.

**Mapping list** (``prop['prop2_name']``).
Most properties belong to this type.
There are two columns in the data file.
Key ``x`` stores the list of spanwise locations (first column), while ``y`` stores the list of property values (second column).

**Others** (``prop['prop3_name']``).
The rest data blocks that do not belong to the previous two types, such as 'BMISC'.









Read the load data (``readRcasLoad``)
---------------------------------------

..  code-block:: python

    import msgd.ms.rcas as mmr
    force, moment = mmr.readRcasLoad('force.csv', 'moment.csv')

Returned values of this function are Python dictionaries having the following data layout.

..  note::

    ``force`` and ``moment`` have the same layout.

..  code-block:: python

    force = {
        'node_id': [],
        'case_1': {
            'x': [
                [a1, xn1, xn2, xn3, ...],
                [a2, xn1, xn2, xn3, ...],
                ...
            ],
            'y': [],
            'z': []
        },
        'case_2': {...},
        ...
    }


``node_id``
    This is a list of nodal IDs.
    They are parsed from the header of the file.
    ID is the number after the keyword 'NODE'.

``case_1``, ``case_2``, ...
    Case ID (first column) in the file.

``x``, ``y``, ``z``
    Component (second column in the file) of the load.
    Each of them is a list of loads for all nodes but one azimuth angle.
    In other words, each item in the list corresponds to a row in the file.

    For example, ``force['case_1']['x'][0]`` is ``[a1, xn1, xn2, xn3, ...]``, which means Fx at node 1 (``xn``), node 2 (``xn2``), node 3 (``xn3``) and so on for the first azimuth angle (``a1``), say 15 degrees.
