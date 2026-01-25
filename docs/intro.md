---
marp: true
paginate: true
---

# Why DV Flow
- Complex workflows need orchestration
  - Multiple tools processing same data
  - Long processing times makes work-avoidance critical  
  - Dependencies can be complex
- DV Flow provides data-driven, parameterizable workflows
  - Silicon design & verification
  - Agentic AI workflows
  - Build automation

---

# DV Flow Key Elements
- Task-flow specification -- YAML in one or more files
- Processing tools -- Development, execution, analysis, etc
- Task libraries -- Collections of ready-to-use domain-specific tasks

---

# DV Flow Key Concepts
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

# DV Flow Use Cases
- **Silicon Design & Verification**: Compile, simulate, verify HDL designs
- **Agentic Workflows**: Encapsulate prompts, context, tools as reusable tasks
- **Build Automation**: Orchestrate complex multi-step processes

---

# DV Flow Execution
- Tasks and `need` relationships form a Directed Acyclic Graph (DAG)
- Tasks are executed in dependency order
- Tasks without shared dependencies can be executed concurrently


