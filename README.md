# Julia-Embedded-Master

<p align="center">
  <img src="https://github.com/Julia-Embedded/Julia-Embedded-Master/blob/master/logo/Julia-Embedded-logo-small.png" alt="Julia-Embedded-Logo" height="350"/>
</p>

An organization for bringing Julia to embedded processors.

# Goals 
 * Building executable
 * Making lib/dll libraries.
 * A lot of the drivers and libraries are written in C, so we also can try embedding Julia in an already written C code (like writing the main computational function in Julia).
 * Building on desktop (Windows, etc) for ARM.

# Background
Julia is a high-level language with convenient interfaces for libraries in other languages (e.g. C, C++, etc), and also it is possible to embed Julia in an already written project.

# Motivation
We were interested to try to build and try some programs using Julia for embedded processors. Also, make some examples for others to use as templates for embedded programming in different situations.
As Julia 1.2 added 32bit binaries we decided to start this work:
   * all of the ARM Cortex-M processors (https://en.wikipedia.org/wiki/ARM_Cortex-M) which are highly used in many embedded applications are 32 bit.
   * all of the ARM Cortex-R processors (https://en.wikipedia.org/wiki/ARM_Cortex-R) for mission-critical applications are 32 bit.
   * a lot of ARM Cortex-A processors are 32 bit (https://en.wikipedia.org/wiki/ARM_Cortex-A).
However, this work will be useful for any embedded system.


# Discourse Forum
https://discourse.julialang.org/t/bring-julia-code-to-embedded-hardware-arm/19979/27
