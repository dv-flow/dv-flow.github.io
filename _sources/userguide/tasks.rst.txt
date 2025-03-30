#####
Tasks
#####

Tasks are the fundamental unit of behavior in a DV-Flow specification. Tasks
accept data from tasks that they depend on, and produce data to be used by
dependent tasks. Tasks may have local parameters to control operation.

The implementation of a task is required to perform three key tasks:

* Compute dependencies -- Specifically, determine whether the task must
  perform work. Tasks typically save a 'memento' with the system that
  is used by future evaluations of the task.
* Perform work -- The task implementation must perform the desired
  data transformation when required. Usually this involves invoking
  another tool, such as a compiler. When work is performed, the task
  may produce markers to communicate the location of errors, warnings,
  or other key information.
* Produce output -- Tasks are required to pass data output data
  to their successor tasks independent of whether the task performed
  a data transformation.

Using Tasks
===========

Most tasks are built on top of another existing task. 

* Base task (uses)

* Setting parameters (with)

* Specifying dependencies (needs)



Using Compound Tasks
====================

Compound tasks allow a task to be defined in terms of a set 
of other tasks. In many cases, this allows more-advanced behavior
to be created without the need to provide a programming-language
implementation for the task.


Compound-Task Strategy
----------------------


Compound tasks support 


