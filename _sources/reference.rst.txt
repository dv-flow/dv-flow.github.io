###################
Flow-Spec Reference
###################

Conventions
###########

The reference documentation uses a few conventions when specifying the
capabilities of various aspects of the specification:

* **refstring** - A string where parameter and expression references (ie ${{ ... }})
  are expanded. 
* **string** - A literal string

Packages
########

A package file defines content under a `package` root element. The `name` element 
is required. Other elements are optional. 


.. code-block:: yaml
    :caption: Minimal package definition

    package:
      name: my_package

An outline of the package schema is shown below. Please see the following sections
for more information about key items:

* Datasets
* Tasks

.. list-table::
    :header-rows: 2
    :widths: auto

    * - Schema: 
      - #/defs/PackageDef
      -
    * - Item 
      - Type
      - Description
    * - name
      - string
      - Name of the package
    * - desc
      - string
      - Short description of the package
    * - doc
      - string
      - Documentation of the package content
    * - uses
      - string
      - Name of the base package
    * - with
      - list[refstring | ParamDef]
      - Package parameters
    * - imports
      - list[refstring]
      - External packages to load
    * - tasks
      - list[TaskDef]
      - Task definitions
    * - datasets
      - list[DatasetDef]
      - Dataset definitions
    * - fragments
      - list[refstring]
      - Package fragment files
A package file defines content under a `package` root element. The `name` element 
is required. Other elements are optional. 


.. code-block:: yaml
    :caption: Minimal package definition

    package:
      name: my_package

Uses
====

A package inherits from a base package via the `uses` element. All elements from the base
package become elements of the inheriting package.

.. code-block:: yaml
    :caption: Package inheritance

    # my_base_pkg.yaml
    package:
      name: my_base_pkg
      tasks:
      - name: my_t1

    # my_ext_pkg.yaml
    package:
      name: my_ext_pkg
      uses: my_base_pkg
      imports:
      - my_base_pkg.yml
      tasks:
      - name: my_t2

In the example above, `my_ext_pkg` contains two tasks: `my_t1` and `my_t2`. 

With
====

A package declares and configures package-local parameters using the `with` section.

.. code-block:: yaml
    :caption: Package parameter declaration

    package:
      name: my_package
      with:
      - name: p1
        type: str
        value: abc

For more information about declaring and using parameters, see the `Parameters` section.

Imports
=======

Packages are explicitly loaded from a file using the `imports` section. Each entry in this
section is a path to a package file. The path may be absolute or relative. Relative paths
are resolved:

* Relative to the directory containing the current file
* Relative to the directory containing the root package file

Variable references are supported.

.. code-block:: yaml
    :caption: Package import with an environment-rooted path

    package:
      name: my_package
      imports:
      - ${{ env.ANCHOR_my_uvc }}/flow.yaml

.. code-block:: yaml
    :caption: Package import with a relative path

    package:
      name: my_package
      imports:
      - import/my_ip/flow.yaml


Package Fragments
#################

Package fragment files specify additional content. Most package elements can be
declared in a fragment, with the exception of the package `name`, 
`uses` (base package), and `with` (package parameters).

.. code-block:: yaml
    :caption: Package fragment

    fragment:
      imports:
      - ../my_file.yaml
      tasks:
      - name: T1
        # ...


.. list-table::
    :header-rows: 2
    :widths: auto

    * - Schema: 
      - #/defs/FragmentDef
      -
    * - Item 
      - Type
      - Description
    * - imports
      - list[refstring]
      - External packages to load
    * - tasks
      - list[TaskDef]
      - Task definitions
    * - datasets
      - list[DatasetDef]
      - Dataset definitions
    * - fragments
      - list[string]
      - Package fragment files

Task Definition
===============

.. jsonschema:: _build/flow.dv.schema.json#/defs/RundirE
.. jsonschema:: _build/flow.dv.schema.json#/defs/PackageSpec
.. jsonschema:: _build/flow.dv.schema.json#/defs/TaskDef


.. jsonschema:: _build/flow.dv.schema.json#/defs/PackageImportSpec
.. jsonschema:: _build/flow.dv.schema.json#/defs/TypeDef
.. jsonschema:: _build/flow.dv.schema.json#/defs/StrategyDef
.. jsonschema:: _build/flow.dv.schema.json#/defs/ListType
.. jsonschema:: _build/flow.dv.schema.json#/defs/MapType
.. jsonschema:: _build/flow.dv.schema.json#/defs/ComplexType
.. jsonschema:: _build/flow.dv.schema.json#/defs/ParamDef


