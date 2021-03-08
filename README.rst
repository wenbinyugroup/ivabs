Intruduction 
---------------

**iVABS** (namely integrated VABS), is a versatile design framework for composite slender structures such as helicopter rotor blades, wind turbine blades, high aspect ratio wings, bridges, shafts, etc. This framework bundles **PreVABS**, **VABS**, **GEBT**，**Dakota**, along with many other scripts for integration among these codes and possibly other codes. All the codes are open source except VABS which is commerical code and a trial license or commerical license can be requested from `AnalySwift <http://analyswift.com/software-trial/>`_.  

**PreVABS** is a versatile preprocessor to generate detailed composite sections based on a few design parameters including sectional geometry, topology, and material. 

**VABS** is a world-known cross-sectional analysis code to to model composite slender structures as beams. It is based on decades of university research (Georgia Tech/Utah State/Purdue) sponsored by US Army.  

**GEBT** is a simple geometrical exact nonlinear beam analysis code for computing linear or nonlinear, static or dynamic behavior of composite beams. This code can be replaced with more sophicated codes such as `MBDyn<https://public.gitlab.polimi.it/DAER/mbdyn>`_, `RCAS<https://www.flightlab.com/grcas.html`_, `DYMORE<dymoresolutions.com>`_.

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

