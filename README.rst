**iVABS** (namely integrated VABS), is a design framework for composite slender structures such as helicopter rotor blades, wind turbine blades, high aspect ratio wings, bridges, 
            shafts, etc. This framework bundles **PreVABS**, **VABS**, **GEBT**, **Dakota**, along with scripts for integration among these codes and other related codes. All the codes are open source except VABS which is commerical code and a license can be requested from `AnalySwift <http://analyswift.com/software-trial/>`_.  **PreVABS**, **VABS**, **GEBT**, and integration scripts are developed by `Prof. Wenbin Yu's research group <https://cdmhub.org/groups/yugroup>`_. **Dakota** is developed by the `Sandia National Lab <https://dakota.sandia.gov/>`_. 

  **PreVABS** is a versatile preprocessor to generate detailed composite sections based on a few design parameters including sectional geometry, topology, and material. 

**VABS** is a world-known cross-sectional analysis code to to model composite slender structures as beams. It is based on decades of university research (Georgia Tech/Utah State/Purdue) sponsored by US Army.  

**GEBT** is a geometrical exact nonlinear beam analysis code for computing linear or nonlinear, static or dynamic behavior of composite beams. This code can be replaced with more sophicated codes such as `MBDyn <https://public.gitlab.polimi.it/DAER/mbdyn>`_, `RCAS <https://www.flightlab.com/grcas.html>`_, `DYMORE <http://www.dymoresolutions.com>`_, etc.

**Dakota** is a multilevel, parallel, object-oriented framework for design optimization, parameter estimation, uncertainty quantification, and sensitivity analysis. 
