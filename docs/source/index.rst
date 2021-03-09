.. v4d documentation master file, created by
   sphinx-quickstart on Tue May 30 13:54:05 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to iVABS Documentation
=================
iVABS (namely integrated VABS), is a design framework for composite slender structures such as helicopter rotor blades, wind turbine blades, high aspect ratio wings, bridges, shafts, etc. This framework bundles PreVABS, VABS, GEBT, Dakota, along with scripts for integration among these codes and other related codes. All the codes are open source except VABS which is commerical code and a license can be requested from `AnalySwift <http://analyswift.com/software-trial/>`_.  PreVABS, VABS, GEBT, and integration scripts are developed by `Prof. Wenbin Yu's research group <https://cdmhub.org/groups/yugroup>`_. Dakota is developed by the `Sandia National Lab <https://dakota.sandia.gov/>`_. 

PreVABS is a versatile preprocessor to generate detailed composite sections based on a few design parameters including sectional geometry, topology, and material. 

VABS is a world-known cross-sectional analysis code to to model composite slender structures as beams. It is based on decades of university research (Georgia Tech/Utah State/Purdue) sponsored by US Army.  

GEBT is a geometrical exact nonlinear beam analysis code for computing linear or nonlinear, static or dynamic behavior of composite beams. This code can be replaced with more sophicated codes such as `MBDyn <https://public.gitlab.polimi.it/DAER/mbdyn>`_, `RCAS <https://www.flightlab.com/grcas.html>`_, `DYMORE <http://www.dymoresolutions.com>`_, etc.

`Dakota <https://dakota.sandia.gov/>`_ is a multilevel, parallel, object-oriented framework for design optimization, parameter estimation, uncertainty quantification, and sensitivity analysis. 

Table of Contents
===================
.. toctree::
   :hidden:
   :maxdepth: 2
   :caption: iVABS
   
   ivabs/install
   ivabs/examples 

.. toctree::
   :hidden:
   :maxdepth: 2
   :caption: PreVABS

   prevabs/install
   prevabs/run
   prevabs/tutorial
   prevabs/guide
   prevabs/examples
   prevabs/changelog
   prevabs/xml
   prevabs/references


.. toctree::
   :hidden:
   :maxdepth: 2
   :caption: MSGPI 

   msgpi/sg_structuregene
   msgpi/sg_materialsection
   msgpi/methods
   msgpi/beam
   msgpi/beam_methods
   msgpi/utils
