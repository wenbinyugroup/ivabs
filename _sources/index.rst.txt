.. v4d documentation master file, created by
   sphinx-quickstart on Tue May 30 13:54:05 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to iVABS Documentation
=================
iVABS (namely integrated VABS), is a design framework for composite slender structures such as helicopter rotor blades, wind turbine blades, high aspect ratio wings, bridges, shafts, etc. This framework bundles :ref: `PreVABS`, VABS, GEBT, Dakota, along with MSGPI for integration among these codes and other codes. All codes are open source except VABS which is a commerical code and a license can be requested from `AnalySwift <http://analyswift.com/software-trial/>`_.  PreVABS, VABS, GEBT, and MSGPI are developed by `Prof. Wenbin Yu's research group <https://cdmhub.org/groups/yugroup>`_. Dakota is developed by the `Sandia National Lab <https://dakota.sandia.gov/>`_. 

iVABS can be downloaded from `its github repository <https://github.com/wenbinyugroup/ivabs/releases>`_. The detailed instruction is given in Download and Installation. 

.. _PreVABS: PreVABS is a versatile preprocessor to generate detailed composite sections based on a few design parameters including sectional geometry, topology, and material. 

VABS is a world-known cross-sectional analysis code to to model composite slender structures as beams. It is resulting from  decades of university research (Georgia Tech/Utah State/Purdue) sponsored by US Army.  

GEBT is a geometrical exact nonlinear beam analysis code for computing linear or nonlinear, static or dynamic behavior of composite beams. This code can be replaced with more sophicated codes such as `MBDyn <https://public.gitlab.polimi.it/DAER/mbdyn>`_, `RCAS <https://www.flightlab.com/grcas.html>`_, `DYMORE <http://www.dymoresolutions.com>`_, etc.

`Dakota <https://dakota.sandia.gov/>`_ is a multilevel, parallel, object-oriented framework for design optimization, parameter estimation, uncertainty quantification, and sensitivity analysis. 

MSGPI contains all the Python scripts needed for integrating all the codes in iVABS. Thus, to make use of the full functionalities of iVABS, `Python 3.0 <https://www.python.org/>`_ or later versions should have been installed and is working on your computer. 

Contributing
===================

We would love to have you help us improve the iVABS documentation. You can contribute to the iVABS documentation in the following ways:

#. You can comment on specific page on the `iVABS documentation website <http://wenbinyugroup.github.io/ivabs>`_. 
#. Add an inssue to this project.
#. Participate in the discussions regarding this project. 
#. Modify or contribute new files to this project.  

License
=============

* iVABS (excluding VABS) and its documentation is copyrighted (C) 2021- by Wenbin Yu, Su Tian, Haodong Du, and Fei Tao and is distributed under the terms of the GNU General Public License (GPL) (version 2 or later, with an exception to allow for easier linking with external libraries).
* VABS is a code commercialized by `AnalySwift <https://analyswift.com/>`_. 
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
