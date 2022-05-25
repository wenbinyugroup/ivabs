Components
============

PreVABS is a preprocessor to generate composite sections with ply-level details based on a few design parameters including sectional geometry, topology, and material. 

VABS is a cross-sectional analysis code to to model composite slender structures as beams.
It is resulting from  decades of university research (Georgia Tech/Utah State/Purdue) sponsored by US Army.  

GEBT is a geometrical exact nonlinear beam analysis code for computing linear or nonlinear, static or dynamic behavior of composite beams.
This code can be replaced with more sophicated codes such as `MBDyn <https://public.gitlab.polimi.it/DAER/mbdyn>`_, `RCAS <https://www.flightlab.com/grcas.html>`_, `DYMORE <http://www.dymoresolutions.com>`_, `CAMRAD II <http://www.johnson-aeronautics.com/>`_, etc.

`Dakota <https://dakota.sandia.gov/>`_ is a multilevel, parallel, object-oriented framework for design optimization, parameter estimation, uncertainty quantification, and sensitivity analysis.
This code can be easily replaced by another design and optimization framework such as `OpenMADO <https://openmdao.org/>`_.

MSGPI is a collection of phython scripts for integrating the codes needed in iVABS and the scripts can be modified to integrate other codes.
To make use of MSGPI, `Python3 <https://www.python.org/>`_ along with necessary packages (particularly ``numpy``, ``scipy``, and ``pyyaml``) should be installed and working on your computer. 

