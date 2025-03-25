---
marp: true
paginate: true
---

# Why DV-Flow
- Software languages often have a companion build tool 
  - C/C++ - Make, CMake
  - Java - ANT, Gradel, etc
  - ...
- Silicon design engineering also have unique requirements
  - Many tools processing same source
  - Long processing times makes work-avoidance critical
  - Dependencies can be complex

---

# DV-Flow Key Elements
- Task-flow specification -- YAML in one or more files
- Processing tools -- Development, execution, analysis, etc
- Task libraries -- Collections of ready-to-use application-specific tasks

---

# DV-Flow Key Concepts
- Tasks - Specifies data collection and manipulation steps and dependencies
- Packages - Organizes tasks/types and supports variants
- Dataflow - Tasks input, output, and operate on `parameter sets` (eg file lists)

```
package:
  name: my_ip
  tasks:
  - name: rtlsrc
    uses: std.FileSet
    with:
      base: src/rtl
      include: "*.sv"
  - name: sim_img
    uses: hdlsim.vlt.SimImage
    needs: [rtlsrc]
```

---

# DV-Flow Execution
- Tasks and `need` relationships form a Directed Acyclic Graph (DAG)
- Tasks are executed in dependency order
- Tasks without shared dependencies can be executed concurrently



