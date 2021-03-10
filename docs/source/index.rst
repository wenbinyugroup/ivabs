.. v4d documentation master file, created by
   sphinx-quickstart on Tue May 30 13:54:05 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to iVABS Documentation
=================
iVABS (namely integrated VABS), is a design framework for composite slender structures such as helicopter rotor blades, wind turbine blades, high aspect ratio wings, bridges, shafts, etc. This framework bundles PreVABS, VABS, GEBT, Dakota, along with MSGPI for integration among these codes and other codes. PreVABS, VABS, GEBT, and MSGPI are developed by `Prof. Wenbin Yu's research group <https://cdmhub.org/groups/yugroup>`_. Dakota is developed by the `Sandia National Lab <https://dakota.sandia.gov/>`_. 

For download and install iVABS, refer to :doc:`ivabs/install`.

PreVABS is a preprocessor to generate detailed composite sections based on a few design parameters including sectional geometry, topology, and material. 

VABS is a  cross-sectional analysis code to to model composite slender structures as beams. It is resulting from  decades of university research (Georgia Tech/Utah State/Purdue) sponsored by US Army.  

GEBT is a geometrical exact nonlinear beam analysis code for computing linear or nonlinear, static or dynamic behavior of composite beams. This code can be replaced with more sophicated codes such as `MBDyn <https://public.gitlab.polimi.it/DAER/mbdyn>`_, `RCAS <https://www.flightlab.com/grcas.html>`_, `DYMORE <http://www.dymoresolutions.com>`_, etc.

`Dakota <https://dakota.sandia.gov/>`_ is a multilevel, parallel, object-oriented framework for design optimization, parameter estimation, uncertainty quantification, and sensitivity analysis. 

MSGPI is a collection of phython scripts for integrating the codes needed in iVABS and the scripts can be modified to integrate other codes. To make use of the full functionality of iVABS, `Python3 <https://www.python.org/>`_ along with necessary packages (particularly ``numpy`` and ``matplotlib``) should be installed and working on your computer. 


Contributing
===================

We would love to have you help us improve the iVABS documentation. You can contribute to the iVABS documentation in the following ways:

#. You can comment on specific page on the `iVABS documentation website <http://wenbinyugroup.github.io/ivabs>`_. 
#. `Add an issue <https://github.com/wenbinyugroup/ivabs/issues/new>`_ for bug reports or feature request. You need to signup on github. 
#. `Start a new discussion <https://github.com/wenbinyugroup/ivabs/discussions/new>`_ if you need help running the program. You need to signup on github. 
#. Modify existing files or contribute new files to `the github repository <https://github.com/wenbinyugroup/ivabs>`_.  You need to signup on github and join the project team. 
 
License
=============

* iVABS (excluding VABS) and its documentation is copyrighted (C) 2021- by Purdue Research Foundation and is distributed under the terms of the GNU General Public License (GPL) (version 2 or later, with an exception to allow for easier linking with external libraries).
* VABS is a commercial code and a trial or paid license can be requested from `AnalySwift <http://analyswift.com/software-trial/>`_.
* iVABS makes use of two open source codes: `Gmsh <https://gmsh.info/>`_  and `Dakota <https://dakota.sandia.gov/>`_. 


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
