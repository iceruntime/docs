# How it works

**NOTE**: This project is very early in its design phase and this document may change relatively frequently as we try to work out the best overall structure and tools/frameworks/languages that we want to use. Also keep in mind that this document is written in a way that suggests that ICE is already implemented, but at the moment this is just a glimpse into the future which we aim to bring about.

ICE is an infrastructure provider for dev toolchains. Its core function is to provide primitives for [package management](), [caching]() and [incremental computation]() The idea is that with ICE, language designers can focus on the backend of their language while utilizing the power of ICE for easily dealing with frontend matters.

The benefits are threefold:
 - Easy interop with other ICE-languages.
 - Unification of developer tooling.
 - Integration with the Nix ecosystem.

### Sounds good! How would I use ICE for my new language?

First, you have to make sure that there is a [typing provider plugin]() available for the language(s) you want to implement your new language in. Implement your backend pipeline steps such as module resolution, typechecking and compilation. Then compile them into a [function plugin]() which can be used from ICE. Finally, write the code which glues all your pipeline steps together in one of the supported [ICE-languages]().

### What if I want to use ICE for my already existing language?

Theoretically, ICE is intended to be highly modular, but its features are still designed around it being the main entry point of a language toolchain. This means that to reap most of the benefits of the ICE ecosystem, you are going to have to use ICE as a thin layer around your toolchain. Alternatively, you could use ICE as a driver for a part of your pipeline.

Depending on your goals, various solutions are possible, contact us to discuss!

## Features

ICE aims to provide for all developer toolchain needs. Use ICE to take care of all state and network related problems and focus on developing the core aspects of your toolchain. Additionally, you get interop with other ICE-based tools almost for free!

### Package management
Use [Nix]() infrastructure to manage your packages and other build artifacts. ICE provides abstractions over Nix store operations and allows you to manage system libraries and your own packages in a uniform way. The full power of Nix derivations is available if needed. Read the [details page]() for more.

### Parsing
ICE provides an easy way for specifying grammars, and you can automatically generate parsers using tools like [treesitter]() or [happy](). The parser is included effortlessly in your pipeline, independent of the programming language you use for other transformations. Read the [details page]() for more.

### Caching
The result of every ICE function is transparently cached on disk if the ICE runtime determines it beneficial to do so. The caching is all done via Nix which means that it can be easily shared with other developers, improving the build experience of everyone. Read the [details page]() for more.

### Incremental computation
ICE has an intrinsic concept of diff-based computation, i.e., every ICE function gets passed enough information to only recompute the parts which changed. This makes it ideal as runtime for typechecking workloads where users typically only change local parts of their program. ICE provides the unopinionated substrate on which incremental computation can happen, and every ICE function can implement it in its own way. See the [dia research project]() whose goal is a language in which incremental computation instructions can be automatically generated. Read the [details page]() for more.

### Language agnostic
ICE is the glue code around your pipeline steps, which can be implemented in whichever language you choose (as long as a [type provider plugin]() exists). In fact, you can combine multiple languages easily and due to incremental computation, the communication cost between them is kept at a minimum! Read the [details page]() for more.


## ICE ecosystem

The architecture of ICE is very modular, which means that its various constituents can be iterated upon individually.

### icecore library implementations
The core primitives of ICE are specified in the [icecore]() interface. Any implementation which adheres to the specification can be used by the other components of ICE. We provide the [`icecore-standard`]() implementation. An icecore library can be used like any other C-library, but is meant to be used from icecontrol languages which provide a proper typesystem to guarantee type safety.

### icecontrol languages
The first `icecontrol` language is PureScript, with a dedicated [`PureIce`]() backend. A dependently typed `icecontrol` language is planned based on [`Kami`](). Dev toolchain developers write their glue code in an `icecontrol` language, and their individual transformation steps as ICE-functions.

### ICE-functions

### ICE-type providers

### Rei buildsystem









There are the following components:
 - icecore-interface (a formal specification of the interface
   that an icecorelib has to expose)
 - beam-icecorelib
    - an implementation of the icecore-interface with the BEAM virtual machine (erlang, elixir)
 - purescript-on-ice
    - exposing the icecorelib to purescript
    - in the best case this can take any icecore-interface implementation
 - a future higher level language which embeds an icecore-interface
 - ice-plugins
    - ice type providers
    - ice functions
 - rei buildsystem: types for Nix packages



