.. _section-input_guide:

Guide to Main Input File
========================

The main input file uses the format `YAML <https://yaml.org/>`_.

Overall layout of the main input file:

..  code-block:: yaml

    name: "composite_blade_design"
    setting:
        # setting block
    design:
        # design parameter block
    model:
        # model block
    analysis:
        # analysis steps block
    study:
        # design study block




..  toctree::
    :maxdepth: 1

    input_guide/intro_yaml
    input_guide/input_design
    input_guide/input_analysis
    input_guide/input_study

