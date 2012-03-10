# Fundamental RTL #

## The Module ##

---
type: figure
caption: "Module"
file: ../artwork/singlemodule.png
reference: fig:module
align: center
...

A module is an encapsulation of a piece of hardware.  All of the RTL we write
will be defined inside one or more modules. A module can have zero or more ports
which are used to expose the internal signals.  All signals between modules
must go through the module's ports as one module can't see the internal signals
of another module except through the module's ports.

---
type: figure
caption: "Connected Modules"
file: ../artwork/modules.png
reference: fig:modules
align: center
...

Verilog allows you to define any number of modules in a single file, but a good
convention to follow is to only define one module per file and name the module
the same as the filename.  For instance a module that describes the hardware
for a UART core might be named "uart_core", and the filename would be
"uart_core.v".

Hierarchy in a design is created by instantiating modules inside of other
modules. It is a **very** good idea to break up your designs into small
functional blocks that can be tied together to form the full functionality.

Not only does it concisely describe the individual functions of the
design it also makes debugging problems much easier for the designer and anyone
else who maintains the code.


### Comment Blocks
