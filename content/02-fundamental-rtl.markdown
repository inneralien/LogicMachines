# Fundamental RTL #

## The Module ##

![Figure 1-X: Module](../images/module.png)

A module is an encapsulation of a piece of hardware.  All of the RTL we write
will be defined inside one or more modules. A module can have zero or more ports
which are used to expose the internal signals.  All signals between modules
must go through the module's ports as one module can't see the internal signals
of another module except through the module's ports.

![Figure 1-X: Modules](../images/modules.png)

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

Figure 1-X shows a diagram of one module that instantiates two other modules.

![Figure 1-X: Module Hierarchy](../images/hierarchy.png)

Listing 1-X shows an empty module that does absolutely nothing. It has no ports
and no functionality, but it is syntactically correct and will compile.

Listing 1-X: Empty Module
~~~ {.verilog}
    module simple ();
    endmodule
~~~

### Ports List ###
A modules ports are the interface to the logic contained within, and
are defined in the ports list.  It's easy to end up with an ugly looking
ports list, but we feel the method shown in 
Listing 1-X is clean and readable.

Thankfully the Verilog 2001 standard introduced ANSI C style ports list which
greatly reduces the redundant typing previously required to define signals
attached to ports.  The direction, type, range, and signal name of each port
can all be defined on a single line as shown in
Listing 1-X.  All modern simulator and synthesis engines
support ANSI C style ports lists, so utilize this fantastic feature.

Listing 1-X: Module Port Declaration
~~~ {.verilog}
    module simple (
        input  wire         clock,
        input  wire         reset,
        input  wire [3:0]   select,
        output reg  [3:0]   state
        );
~~~

![Figure 1-X: Port Declaration Details](../images/portdecl.png)

### Wires and Regs ###
There are some basic "types" in Verilog.  The two that we will use most are
**wire** and the **reg**  It's good to keep in mind, however, that the only real
"type" is the bit which is nothing more than *1* and *0*.

If you want to make a register you have to first declare the register signal as
a **reg** type or the compiler and synthesizer will give you an error.

The **wire** type is used to declare just what you'd expect, a wire.  A **reg**
is used to declare a signal that is going to be used to build a register.  Both
of these types can consist of one or more bits.  If you want more than one bit
you add a range to the declaraction.  The range of a wire or reg is given
inside square brackes **[MSB:LSB]**.

Declaring a single bit wire looks like the following and has no range:

~~~ {.verilog}
    wire my_wire;
~~~

Declaring an 8-bit wire looks like this:

~~~ {.verilog}
    wire [7:0] my_wire;
~~~

You'll notice that the range is written with the highest number on the
left of the colon and the smallest number on the right of the colon. The
larger number signifies the most significant bit (MSB) **position** and
the smaller number signifies the least significant bit (LSB)
**position** with zero based counting. ^[This is convention.  You can declare a range backwards as **[LSB:MSB]** as well, but it doesn't make much sense]
Take for example the number *8*
written in binary in 
Figure 1-X
as an example of why this
is done. When you write a binary number the MSB is on the left and the
LSB is on the right, so this convention follows.



![Figure 1-X: Bit Positions](../images/bitpositions.png)

Declaring a register is similar to declaring a wire:

~~~ {.verilog}
    reg my_reg;
~~~

And an 8-bit register declaration:

~~~ {.verilog}
    reg [7:0] my_wire;
~~~

The reg type is meant to declare that a signal is going to be used to
build a synchronous register (flip-flop) with a clock input, but there are some
cases where its use will ultimately generate a wire.  I'll show you how to
avoid that situations because making a wire out of something declared as a
register is just as confusing as it sounds.  What this implies is that simply
declaring a signal as a reg doesn't actually generate a register.  A register
is generated inside of an "always" block and is a synchronous device.

### Timescales ###
The first value *1 ns* means that the discrete simulation time steps should be
1 nanosecond.
Any *#* symbol will be a multiple of 1
nanosecond.  If we were to use a *#* delay of 2, *#2*, that would tell the
simulator to wait *2x1ns=2ns* time steps which in this case is 1 ns.

### Summary Points ###

-   A module is an encapsulation of a piece of hardware.

-   One module can only access the internal signals of another module
    via the ports.

-   Only define one module per file.

-   The only real “type” is the bit.

-   A ports direction, type, range and signal name can all be defined on
    a sin line in the ports list.

-   Just declaring a signal as type *reg* doesn't create any hardware.
    Registers are generated inside of an *always* block.


