
# Introduction #

This chapter is an introduction to the basics of building hardware via the
hardware description language (HDL) Verilog. The goal of this book is to show
many of the fundamental 
[design patterns](http://en.wikipedia.org/wiki/Software_design_pattern)
that will generate functional, synthesizable hardware for use in FPGAs, CPLDs
and ASICs.

## Describing Hardware ##

>You are not writing software, you are describing hardware.

The sentence above conveys the most important principle you can take
away from this book. I can’t overstate just how important it is, and it
is a mindset that must be embraced completely when designing digital
hardware. If you remember nothing else you read here, remember this
principle.

Unlike programming languages which have functions or methods that get
called in some particular sequence, in a hardware description language
(HDL) each construct is used to describe a physical piece of hardware
that you want to build. HDL code is a blueprint of a physical machine
whereas software is the instructions on how to operate it.

The methodologies used to create digital hardware certainly have many
things in common with a software development flow even using some of the
same tools, but that’s where the similarities end. In Verilog you don’t
call functions or pass arguments, you instantiate modules, build gates
and registers and connect them together with wires. It’s like describing
a printed circuit board using a text file instead of a schematic. A PCB
has components like ICs, switches, connectors, LEDs and copper traces
connecting them all together. Digital logic is the same but the
components are flip-flops, multiplexers and gates.

## RTL ##

RTL, or Register Transfer Level, is the technical term for HDL code
written in such a way that it can be synthesized into functional working
gates and built into an ASIC or downloaded into an FPGA. This book is
about writing RTL and will describe and show examples of some best
practices used to write code that **will** function as physical
hardware. Because in the end what matters is creating hardware that
works.

## Tools of the Trade ##

* Text editor
* Simulator
* Waveform viewer
* Synthesis engine

