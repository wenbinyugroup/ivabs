**iVABS**, standing for integrated VABS, is a versatile design framework for composite slender structures such as helicopter rotor blades, wind turbine blades, high aspect ratio wings, bridges, shafts, etc. These structures are usually modeled as beams. 

**iVABS** uses **PreVABS** as a versatile preprocessor to generate detailed composite sections based on a few design parameters including sectional geometry, topology, and material. 

**iVABS** uses **VABS**, a world-known cross-sectional analysis code based on decades of  research at Georgia Tech, Utah State, and Purdue, to model the composite slender structures as a beam. 

bundles  **PreVABS + VABS + gmsh + msgpi + GEBT 
+ Dakota(optional)** . **PreVABS** is a parametrized composite design tool. 
**VABS** is a commercial code for cross-sectional property analysis. **msgpi**
is a Python interface for **VABS**. **GEBT** is a beam structural analysis tool.
**PreVABS**, **VABS**, **msgpi**, and **GEBT**  are developed in Prof. Yu's 
group. **Gmsh** is an open source CAD software. **Dakota** is an open source 
tool for optimization developed by Sandia national lab.

Installation Instructions
-------------------------

It is recommended to use iVABS bundle installer. It provides all the packages
altogether.

1. Download from `Github release page <https://github.com/wenbinyugroup/ivabs/releases>`_.

2. Follow instructions in the Documentation.

Documentation and tutorials
---------------------------

For the documentation and tutorials, see the `iVABS Documentation <http://wenbinyugroup.github.io/ivabs>`_.

You can also download `pdf documentation <https://github.com/wenbinyugroup/ivabs/raw/main/docs/build/latex/PreVABSManual.pdf>`_ for PreVABS.

