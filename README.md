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

# Notes on Cross-compiling and static compilation 

Here are some miscellaneous notes on cross-compiling and static compilation in Julia:

* *CUDAnative* -- [CUDAnative](https://github.com/JuliaGPU/CUDAnative.jl) is the state of the art for cross-compiling to a limited platform. It uses [LLVM.jl](https://github.com/maleadt/LLVM.jl) to help generate appropriate LLVM code. I've copied the approach for [WebAssembly](https://github.com/tshort/ExportWebAssembly.jl) (still very limited or nonworking). This approach is also being used for [AMD GPU's](https://github.com/JuliaGPU/AMDGPUnative.jl). This approach works great, but compatible Julia code is very limited. There has been the talk of separating out the codegen portions of CUDAnative into a separate package, but it hasn't happened, yet.

* *PackageCompiler / tree shaking* -- The approach to static compilation that runs the most code is probably with something like [PackageCompiler](https://github.com/JuliaLang/PackageCompiler.jl). [Tree shaking](https://en.wikipedia.org/wiki/Tree_shaking) is a way to reduce the size of the compiled system image. See [this](https://github.com/JuliaLang/julia/pull/32273#issuecomment-503628124) for more information. The main hurdles with this approach are that tree-shaking doesn't exist, and it's not set up for cross-compilation.

* *Codegen advances* -- Jameson is working on changes to allow the CUDAnative approach to compile more code: https://github.com/JuliaLang/julia/pull/25984.

* *LLVM support* -- Julia's version of LLVM doesn't include targets of interest for embedded applications.

* *libjulia* -- If used, `libjulia` will need to be cross-compiled. Another option is to write a more minimal version of `libjulia` (hopefully in Julia), and swap out the `ccall`s to `libjulia` functions as needed. 

* *ccalls and cglobal* -- When Julia compiles code CUDAnative style, `ccall` and `cglobal` references get compiled to a direct pointer. These need to be converted to symbol references for later linking. Prototype described [here](https://github.com/tshort/ExportWebAssembly.jl/issues/13).

* *Global variables* -- A lot of code gets compiled with global variables, and these get compiled to a direct pointer. One way to handle this is with a serialize/deserialize approach. Prototype described [here](https://github.com/tshort/ExportWebAssembly.jl/issues/13).

* *Initialization* -- If `libjulia` is used, some init code needs to be run to set up GC and other things. It's not clear how to do that from outside. May need PR's to base Julia to help here.

## Some possibly useful repositories from other languages:
https://github.com/uraimo/buildSwiftOnARM
https://github.com/uraimo/SwiftyGPIO
https://github.com/rust-embedded/docs
https://github.com/micropython/micropython
