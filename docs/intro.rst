############
Introduction
############

DV Flow is a framework for orchestrating data-driven, parameterizable workflows.
Tasks are connected by dataflow, enabling composable and reusable workflow 
definitions across many domains.

Why DV Flow?
============

Many workflow systems are tightly coupled to specific domains or tools. DV Flow
takes a different approach: workflows are specified declaratively in YAML, with
tasks connected by dataflow. This enables:

- **Data-Driven Execution**: Tasks receive data from their dependencies, decoupling
  operations from data providers
- **Parameterization**: Workflows can be specialized through parameters, enabling
  reuse across different configurations  
- **Composability**: Tasks and packages support inheritance and extension

Use Cases
=========

**Silicon Design & Verification**

Originally designed for silicon engineering, DV Flow excels at hardware workflows
where the same source files are processed by multiple tools with different configurations:

* Compile designs with UVM testbenches for simulation-based verification
* Run formal verification with different testbench configurations
* Target synthesis with specific subsets of the design

**Agentic AI Workflows**

DV Flow enables agentic workflows by treating prompts, context, and tools as
reusable tasks:

* Encapsulate prompts and context as parameterizable tasks
* Chain agentic and non-agentic operations in the same workflow
* Run sub-workflows composed of multiple operations

**Build Automation**

Orchestrate complex multi-step build processes with intelligent caching and
dependency tracking.

Core Concepts
=============

DV Flow provides workflow management through three key aspects:

* **Flow Specification** - Processing steps for a given project are captured in a hierarchy
  of YAML files. The flow-specification schema is designed to be tool-independent, such 
  that multiple tools can be implemented that comprehend a flow specification.
* **Task Library** - Processing steps are implemented as `tasks`. Libraries of common tasks
  are defined to cover common cases. External libraries of tasks are supported, such that 
  tools can bundle a task library along with the tool installation.
* **Tools** - The Python implementation of DV Flow Manager is one example of a tool. Other tools
  include development and visualization support in VSCode.



