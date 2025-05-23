##########
Quickstart
##########

==========================
Installing DV Flow Manager
==========================

DV Flow Manager is most-easily installed from the PyPi repository:

.. code-block:: bash

    % pip install dv-flow-mgr


Once installed, DV Flow Mananager can be invoked using the `dfm` command:

.. code-block:: bash

    % dfm --help


===============
Your First Flow
===============

When starting a hardware project, it's often easy to first create a little 
compile script for the HDL sources. Over time, that script becomes larger and
larger until we realize that it's time to create a proper build system for our
design, its testbench, synthesis flows, etc.

A key goal of DV Flow Manager is to be easy enough to use that there is no need
to create the `runit.sh` shell script in the first place. We can start by creating 
a `flow.dv` file and just continue evolving our flow definition as the project grows.

Let's create a little top-level module for our design named `top.sv`:

.. code-block:: systemverilog

    module top;
        initial begin
            $display("Hello, World!");
            $finish;
        end
    endmodule


Now, we'll create a minimal `flow.dv` file that will allow us to compile and 
simulate this module.

.. code-block:: yaml

    package:
        name: my_design

        tasks:
          - name: rtl
            uses: std.FileSet
            with: { type: "systemVerilogSource", include: "*.sv" }

          - name: sim-image
            uses: hdlsim.vlt.SimImage
            with: { top: [top] }
            needs: [rtl]

          - name: sim-run
            uses: hdlsim.vlt.SimRun
            needs: [sim-image]


If we run the `dfm run sim-run` command, DV Flow Manager will:

* Find all files with a `.sv` extension in the current directory
* Compile them into a simulation image
* Run the simulation image

.. code-block:: bash

    % dfm run sim-run

This will compile the source, build a simulation image for module `top`,
and run the resulting image. Not too bad for less than 20 lines of build 
specification.

A Bit More Detail
=================
Let's break this down just a bit:

.. code-block:: yaml

    package:
        name: my_design


DV Flow views the world as a series of *packages* that reference each
other and contain *tasks* to operate on sources.  Here, we have declared 
a new package named my_design.

.. code-block:: yaml
    :emphasize-lines: 5-9

    package:
        name: my_design

        tasks:
          - name: rtl
            type: std.FileSet
            with:
              type: "systemVerilogSource"
              include: "*.sv"

Our first task is to specify the sources we want to process. This is done
by specifying a `FileSet` task. The parameters of this task specify where
the task should look for sources and which sources it should include

.. code-block:: yaml
    :emphasize-lines: 11-15

    package:
        name: my_design

        tasks:
          - name: rtl
            uses: std.FileSet
            with:
              type: "systemVerilogSource"
              include: "*.sv"

          - name: sim-image
            uses: hdlsim.vlt.SimImage
            with:
              - top: [top]
            needs: [rtl]

Next, we use the `SimImage` task to compile the sources into a simulation
image. The `sim-image` task receives the list of files to compile from
the tasks that it depends on -- in this case, the `rtl` task. The `sim-image`
task outputs a path to the directory containing the simulation image.

.. code-block:: yaml
    :emphasize-lines: 17-19

    package:
        name: my_design

        tasks:
          - name: rtl
            uses: std.FileSet
            with:
              type: "systemVerilogSource"
              include: "*.sv"

          - name: sim-image
            uses: hdlsim.vlt.SimImage
            with:
              - top: [top]
            needs: [rtl]

          - name: sim-run
            uses: hdlsim.vlt.SimRun
            needs: [sim-image]

Finally, we run use the `sim-run` task to run the simulation image. This
task takes the output from the `sim-image` task (the simulation image directory)
as input. 

