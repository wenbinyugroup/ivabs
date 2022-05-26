.. v4d documentation master file, created by
   sphinx-quickstart on Tue May 30 13:54:05 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to iVABS Documentation
===============================

iVABS (namely integrated VABS), is a design framework for composite slender structures (also called composite beams) such as helicopter rotor blades, wind turbine blades, high aspect ratio wings, bridges, shafts, etc.
This framework bundles PreVABS, VABS, GEBT, Dakota, along with MSGPI for integration among these codes and other codes.
PreVABS, VABS, GEBT, and MSGPI are developed by `Prof. Wenbin Yu's research group <https://cdmhub.org/groups/yugroup>`_.
Dakota is developed by the `Sandia National Lab <https://dakota.sandia.gov/>`_. The relations of different components are described in the following figure. A brief introduction of different components can be found in the :doc:`ivabs/introduction` page.

..  figure:: /figures/ivabs_components.png
    :name: fig-ivabs_components
    :width: 6in
    :align: center

    The iVABS framework.




Contents
--------


..  toctree::
    :maxdepth: 1


    ivabs/install
    ivabs/getstart
    ivabs/examples
    ivabs/main_input
    ivabs/parameterization
    ivabs/cs_template

   
    ivabs/introduction
    prevabs/index
    msgpi/index









Contributing
-----------------

You are welcome to contribute to the iVABS documentation in the following ways:

#. Suggest edits using the middle icon on the top-right corner of the page you want to change.
#. `Add an issue <https://github.com/wenbinyugroup/ivabs/issues/new>`_ for bug reports or feature requests. 
#. `Start a new discussion <https://github.com/wenbinyugroup/ivabs/discussions>`_ on if you need help running iVABS. 
#. Modify existing files or contribute new files to `the github repository <https://github.com/wenbinyugroup/ivabs>`_.   
 








License
-----------------

* iVABS (excluding VABS) and its documentation is copyrighted (C) 2021- by Purdue Research Foundation and is distributed under the terms of the GNU General Public License (GPL) (version 2 or later, with an exception to allow for easier linking with external libraries).
* VABS is a commercial code and a trial or paid license can be requested from `AnalySwift <http://analyswift.com/software-trial/>`_.
* iVABS makes use of four open source codes: `Gmsh <https://gmsh.info/>`_, `Dakota <https://dakota.sandia.gov/>`_, `RapidXml <http://rapidxml.sourceforge.net/>`_, and `Boost <https://www.boost.org/>`_.









Acknowledgement
----------------

The iVABS team at the Purdue University (PoC: Prof. Wenbin Yu) completed the software development under the BAA project "Efficient High-Fidelity Framework for Structural Design and Optimization of Composite Lifting Bodies" funded by ERDC (PoCs: Dr. Robert Haehnel from U.S. Army ERDC and Dr. Joon W. Lim from U.S. Army DEVCOM AvMC).


