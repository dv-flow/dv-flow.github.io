############
Introduction
############


Many software languages have co-evolved with a build system. For example, C/C++ 
has Make and CMake. Java has ANT, Maven, and Gradle. All of these build systems
provide features that cater to specific ways that a given language is processed,
and provide built-in notions to make setting up simple cases as easy as possible.

One simple example is Make and a single-file C program. Take the code below:

.. code-block:: C
    
    #include <stdio.h>

    int main() {
        printf("Hello, world!\n");
        return 0;
    }


Make provides enough built-in features that are C/C++-specific that we can create
an executable from this source file (assume it's named hello.c) simply by running:

.. code-block:: bash

    make hello

Make knows about C files, it knows about the existance of a C compiler, and it knows
that an executable can be created from a C file of the same name.

Meanwhile, in Silicon Engineering Land...
=========================================

Much like software languages, the languages, tools, and flows used in silicon engineering
have their own unique characteristics. For example, in a silicon-design environment, many 
flows are run over the same source files -- possibly with different configurations.

* We compile our design with a UVM testbench to run dynamic (simulation-based) verification
* We compile our design with different testbenches to run formal verification
* We likely use slightly different subset when targeting synthesis

In addition, we also need to be flexible when it comes to tooling. Over time, we'll likely
use different tools from different providers, and want our projects to adapt as easily as 
possible to a change of tool. It's also likely that we will either want to add new tools
to our environment over time, or adapt our environment to take advantage of new 
productivity-enhancing tool features.

DV Flow provides build-flow management features focused on silicon engineering. 
There are three aspects to the project:

* **Flow Specification** - Processing steps for a given project are captured in a hierarchy
  of YAML files. The flow-specification schema is designed to be tool-independent, such 
  that multiple tools can be implemented that comprehend a flow specification.
* **Task Library** - Processing steps are implemented as `tasks`. Libraries of common tasks
  are defined to cover common cases, such as creating a simulation image. External libraries
  of tasks are supported, such that tools can bundle a task library along with the tool installation.
* **Tools** - The Python implementation of DV Flow Manager is one example of a tool. Other tools
  include development and visualization support in VSCode.






