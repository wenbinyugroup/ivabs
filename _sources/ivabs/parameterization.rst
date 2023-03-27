.. _section-ivabs_parameterization:

Parameterization of Composite Slender Structures
================================================

|msgd| uses a two-level, namely cross-section and blade, parameterization method, as illustrated in :numref:`Fig. %s <fig-ivabs_parameterization>`.
The motivation of using this method is to deal with the challenge of defining a composite structure that is high-fidelity and manufacturable.
Such method should also be able to provide large enough design spaces and accommodate common design language.


..  figure:: /figures/ivabs_parameterization.png
    :name: fig-ivabs_parameterization
    :width: 6in
    :align: center

    The |msgd| parameterization method.




Structural parameterization at the cross-sectional level
----------------------------------------------------------

At the cross-sectional level, VABS requires a high-fidelity and meshed cross-sectional model as the input.
This means that all details in the composite structure must be created properly.
PreVABS is the tool that creates such model data given geometric and material information, such as definitions of airfoil, spar location, material properties, layup schemes, etc.
These inputs can be seen as the "recipe" instructing the code in how to create the cross-section.
Some or all of them can be marked with labels and hence become the cross-sectional level design parameters.
A PreVABS input with such parameter labels can be treated as a design template.
By assigning specific values to those parameters, users can generate a specific PreVABS input file and carry out the cross-sectional analysis.

..  note::

    For more guides to preparing cross-sectional design inputs and templates, please see :ref:`section-prevabs_guide`.




Structural parameterization at the blade level
----------------------------------------------------------

At the blade level, manufacturability requires that designs between neighboring cross-sections should relate to each other, so that the whole structure can be manufactured as designed.
To achieve this, |msgd| uses functions to describe the distributions of cross-sectional level parameters along the blade span.
Coefficients controlling these functions are blade-level design parameters.



