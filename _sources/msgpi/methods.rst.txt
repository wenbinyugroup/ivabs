Methods
=======


Input/Output
------------

.. currentmodule:: msgpi.io

.. highlight:: python

::

    import msgpi.io


Reading
^^^^^^^

.. autosummary::
    :toctree: io/

    iovabs.readVABSIn
    iovabs.readVABSOut
    iovabs.readVABSOutHomo
    iovabs.readVABSOutStrengthRatio
    iosc.readSCIn
    iosc.readSCOut
    iosc.readSCOutBeamProperty
    iosc.readSCOutHomo
    iosc.readSCOutFailure




Writing
^^^^^^^

.. autosummary::
    :toctree: io/

    iovabs.writeVABSIn
    iovabs.writeVABSNodes
    iovabs.writeVABSElements
    iovabs.writeVABSElementOrientations
    iovabs.writeVABSMOCombos
    iovabs.writeVABSMaterials
    iovabs.writeVABSMacroData
    iosc.writeSCNodes
    iosc.writeSCElements
    iosc.writeSCElementOrientations
    iosc.writeSCMOCombos
    iosc.writeSCMaterials
    iosc.writeSCInH
    iosc.writeSCInD
    iosc.writeSCInF
    iosc.writeSCIn









Preprocessing
-------------

.. currentmodule:: msgpi.presg

.. highlight:: python

::

    import msgpi.presg


.. autosummary::
    :toctree: presg/

    readMaterialFromXMLElement
    preSG1D
    preSG









Analysis
--------

.. currentmodule:: msgpi.analysis

.. highlight:: python

::

    import msgpi.analysis


.. autosummary::
    :toctree: analysis/

    solve
    run
    runVABS
    runSwiftComp


