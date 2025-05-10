.. DV Flow Manager documentation master file, created by
   sphinx-quickstart on Tue Jan  7 02:06:13 2025.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

DV Flow
=======

DV Flow defines a build-flow specification targeted at silicon design and 
verification workflows. The specification centers around parameterized 
tasks connected by dataflow. A set of libraries for common tasks is provided.
Users can use these tasks as-is, as well as develop new tasks. Tools are
provided to execute workflows defined in DV Flow syntax and assist with 
their development.

.. mermaid::

    flowchart TD
      A[IP Fileset] --> B[Testbench]
      C[VIP Fileset] --> D[Precompile]
      D --> B
      B --> E[SimImage]
      E --> F[Test1]
      E --> G[Test2]
      E --> H[Test3]

* **DV Flow Manager** - DV Flow execution tool
* **pytest Extension** - Allows DV Flow tasks to be used in pytest unit tests
* **VSCode Extension** - Provides navigation and visualization tools inside VSCode
* **HDLSim Library** - Tasks for compiling and simulating HDL code
* **PSS Library** - Tasks for generating tests from Accellera Portable Stimulus Specification (PSS) models
* **IDE Library** - Tasks for producing filelists to support HDL integrated development environments


.. toctree::
   :maxdepth: 1
   :caption: Contents:

   intro
   quickstart
   userguide/index
   reference
