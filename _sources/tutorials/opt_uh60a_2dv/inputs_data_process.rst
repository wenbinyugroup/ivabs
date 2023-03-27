
.. _sect-input-process:

Data Processing Functions (``data_proc_funcs.py``)
==================================================

.. _sect-input-process-pre:

Pre-processing
--------------

As mentioned in the previous two sections, there is one pre-processing function.

Function ``materialId2Name``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This function converts a material id to a material name.
Dakota generates the integer type material id, while preVABS requires the string type material name.
::

    def materialId2Name(params, results, interface_args):

The mapping relation from an id to a name is defined first in this function::

    mdb = {
        1: 'AS4 12k/E7K8_0.0054',
        2: 'S2/SP381_0.0092',
        3: 'T650-35 12k/976_0.0052',
        4: 'T700 24K/E765_0.0056',
    }

Then, for material selection variable, store the corresponding material name in ``params``::

    params['mn_spar_1'] = mdb[params['mi_spar_1']]
    params['mn_le'] = mdb[params['mi_le']]
    params['mn_te'] = mdb[params['mi_te']]




.. _sect-input-process-post:

Post-processing
---------------

There are two post-processing functions.
One is the overall function that will be called in ``interface.py``.
Another is a specific function that calculates the relative difference between calculated and target beam properties.

Function ``postprocess``
^^^^^^^^^^^^^^^^^^^^^^^^

This is the function that manages all post-processing steps.
::

    def postprocess(params, results, interface_args, cs_inputs, cs_outputs)

No matter how many processing steps there are, the key is to put results into ``results['interim']`` or ``results['final']`` properly and give final results the correct labels and order so that Dakota can retrieve them from ``output.out`` correctly.

First create an empty list to store the differences of each beam properties::

    diff = []

Then loop for each output listed in ``post_process`` in ``interface_args.json``::

    for pp in interface_args['post_process']:

As mentioned in Section: :ref:`sect-input-arguments`, for each output entry, the first item is the output name (descriptor), the second item is a function name, the third one is the arguments for the function, and the last one (if specified) indicates the group of the output, interim or final.
::

    rn = pp[0]
    fn = pp[1]
    args = pp[2]
    result_output = 'final'
    if len(pp) > 3:
        result_output = pp[3]

Then, calculate the output based on the function.
If the function name is ``self``, then the value of the argument is directly copied to the output::

    if fn == 'self':
        r = cs_outputs[args]

If the function name is anything other than ``self``, then we need to execute that function.
Since in this example the only specific function is ``calcRelDiff``, we also need to add the calculated result to the list ``diffs``.
::

    else:
        r = eval(fn)(
            rn, cs_inputs, cs_outputs, interface_args, *args
        )
        diffs.append(r)

Then the result needs to be added to the object ``results`` based on its type, interim or final.
If the type is ``final``, then the pair of result name and value (``[name, value]``) needs to be appended to the list ``results['final']``.
If the type is ``interim``, then the key-value pair (``name: value``) needs to be added to the dictionary ``results['interim']``.
::

    if result_output == 'final':
        results['final'].append([rn, r])
    elif result_output == 'interim':
        results['interim'][rn] = r

Once the loop is done, the last step is to calculate the overall difference, which is also the objective ``diff``.
According to the formula displayed in Section: :ref:`opt`, the objective is actually the infinity norm of the vector containing the five differences.
Hence, this value can be simply calculated using the build-in function ``norm`` in ``numpy``::

    import numpy
    diff = np.linalg.norm(diffs, ord=np.inf)

Since this value is the first one in the response list of Dakota input, it needs to be inserted at the beginning of the final results list::

    results['final'].insert(0, ['diff', diff])




Function ``calcRelDiff``
^^^^^^^^^^^^^^^^^^^^^^^^

This function calculates the relative difference of a specific beam proeprty.
::

    def calcRelDiff(response_name, params, results, json_args, *args, **kwargs)

Here, ``response_name`` is the name of the output (first item of the post-processing entry), such as ``gj_diff``.
``results`` stores the calculated beam properties, which is a dictionary whose keys are those listed in ``beam_properties`` in the JSON file.
``*args`` is the list of arguments specified at the third place of the post-processing entry, such as ``["gj", 24.31e6]``.

Hence, the first item of ``*args`` is the beam property name.
The second one is the target value.
The calculated value is retrieved from ``results`` using the beam property name as the key.
::

    bp_name = args[0]
    target = args[1]
    value = results[bp_name]

In this example, since the desired locations of the shear center and the mass center are measured from the leading edge, some special treatments are needed.

For the horizontal shear center location, the target value is measured from the leading edge, while the calculated value is measured from the model center (quarter chord).
Hence, we need to add the location of the model center measured from the leading edge to the calculated value.
::

    if response_name == 'sc2_le_diff':
        xo2_le = params['chord'] * params['oa2']
        value += xo2_le

For the horizontal mass center location, the target value is measured from the shear center and the calculated value is measured from the model center.
Hence, for the target value, we need to add the location of the shear center measured from the leading edge, and for the calculated value, we need to add the location of the model center measured from the leading edge.
::

    elif response_name == 'mc2_le_diff':
        xo2_le = params['chord'] * params['oa2']
        value += xo2_le
        target += args[2]

Finally, the relative difference is computed as::

    rv = (value - target) / target




Complete file
-------------

.. code-block:: python
    :caption: data_proc_funcs.py
    :name: code-data_process

    import numpy as np

    def materialId2Name(params, results, interface_args):
        mdb = {
            1: 'AS4 12k/E7K8_0.0054',
            2: 'S2/SP381_0.0092',
            3: 'T650-35 12k/976_0.0052',
            4: 'T700 24K/E765_0.0056',
        }
        params['mn_spar_1'] = mdb[params['mi_spar_1']]
        params['mn_le'] = mdb[params['mi_le']]
        params['mn_te'] = mdb[params['mi_te']]


    def postprocess(params, results, interface_args, cs_inputs, cs_outputs):

        diffs = []
        for pp in interface_args['post_process']:
            rn = pp[0]
            fn = pp[1]
            args = pp[2]
            result_output = 'final'
            if len(pp) > 3:
                result_output = pp[3]

            if fn == 'self':
                r = cs_outputs[args]
            else:
                r = eval(fn)(
                    rn, cs_inputs, cs_outputs, interface_args, *args
                )
                diffs.append(r)

            if result_output == 'final':
                results['final'].append([rn, r])
            elif result_output == 'interim':
                results['interim'][rn] = r

        diff = np.linalg.norm(diffs, ord=np.inf)
        results['final'].insert(0, ['diff', diff])

        return


    def calcRelDiff(response_name, params, results, json_args, *args, **kwargs):
        bp_name = args[0]
        target = args[1]

        value = results[bp_name]

        if response_name == 'sc2_le_diff':
            xo2_le = params['chord'] * params['oa2']
            value += xo2_le
        elif response_name == 'mc2_le_diff':
            xo2_le = params['chord'] * params['oa2']
            value += xo2_le
            target += args[2]

        rv = (value - target) / target

        return rv





