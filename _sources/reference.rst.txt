###################
Flow-Spec Reference
###################

File Root Elements
==================

Each `flow.yaml` file either defines a package or a package fragment.
Each package is defined by the content in its root `flow.yaml` file 
and that in any `fragment` files that are specified in the root 
package file or its fragments.

.. code-block:: yaml

    package:
        name: proj1

        # ...

        fragments:
        - src/rtl/flow.yaml
        - src/verif

Each package fragment element specifies either a directory or a file.
If a file is specified, then that file is loaded. It is expected that the
content will be a DV-Flow package fragment. If a directory is specified,
then a top-down search is performed for `flow.dv` files in the subdirectory
tree. 

The structure of a package fragment file is nearly identical to a package
definition. For example:

.. code-block:: yaml

    fragment:
        tasks:
        - name: rtl
          type: std.FileSet
          params:
            include: "*.sv"

Remember that all fragments referenced by a given package contribute to 
the same package namespace. It would be illegal for another flow file
to also define a task named `rtl`.

.. jsonschema:: _build/flow.dv.schema.json#/defs/PackageDef

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


