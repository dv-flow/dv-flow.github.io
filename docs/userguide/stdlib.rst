################
Standard Library
################

std.Exec
========
Runs a shell command.

.. code-block::

    package:
      name: exec.example

      tasks:
      - name: list_dir
        uses: std.Exec
        with:
          command: |
            ls ${{ srcdir }} >> srcdir_files.txt

The example above runs the Unix `ls` command and saves the
output to a text file.

std.FileSet
===========
Creates a 'FileSet' parameter set from a specification. This task is
primarily used to build up list of files for processing by HDL compilation
tools.

.. code-block::

    package:
        name: fileset.example
    
        tasks:
        - name: rtlsrc
            uses: std.FileSet
            with:
              includes: '*.v'
              base: 'src/rtl'
              type: 'verilogSource'

The example above finds all files with a `.v` extension in the `src/rtl` 
subdirectory of the task's source directory. The task emits a FileSet
parameter set having the filetype of `verilogSource`.




