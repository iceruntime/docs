# How it works

**NOTE**: This project is very early in its design phase and this document may change relatively frequently as we try to work out the best overall structure and tools/frameworks/languages that we want to use. Also keep in mind that this document is written in a way that suggests that ICE is already implemented, but at the moment this is just a glimpse into the future which we aim to bring about.

[ICE](https://github.com/iceruntime/ice) is an infrastructure provider for dev toolchains. Its core function is to provide primitives for [package management](), [caching]() and [incremental computation]() The idea is that with ICE, language designers can focus on the backend of their language while utilizing the power of ICE for easily dealing with frontend matters.

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
Use [Nix]() infrastructure to manage your packages and other build artifacts. ICE provides abstractions over Nix store operations and allows you to manage system libraries and your own packages in a uniform way. The full power of Nix derivations is available if needed.

### Parsing
ICE provides an easy way for specifying grammars, and you can automatically generate parsers using tools like [treesitter]() or [happy](). The parser is included effortlessly in your pipeline, independent of the programming language you use for other transformations.

### Caching
The result of every ICE function is transparently cached on disk if the ICE runtime determines it beneficial to do so. The caching is all done via Nix which means that it can be easily shared with other developers, improving the build experience of everyone.

### Incremental computation
ICE has an intrinsic concept of diff-based computation, i.e., every ICE function gets passed enough information to only recompute the parts which changed. This makes it ideal as runtime for typechecking workloads where users typically only change local parts of their program. ICE provides the unopinionated substrate on which incremental computation can happen, and every ICE function can implement it in its own way. See the [dia research project]() whose goal is a language in which incremental computation instructions can be automatically generated.

### Language agnostic
ICE is the glue code around your pipeline steps, which can be implemented in whichever language you choose (as long as a [type provider plugin]() exists). In fact, you can combine multiple languages easily and due to incremental computation, the communication cost between them is kept at a minimum!


## ICE ecosystem

The architecture of ICE is very modular, which means that its various constituents can be iterated upon individually.

### icecore library implementations
The core primitives of ICE are specified in the [icecore]() interface. Any implementation which adheres to the specification can be used by the other components of ICE. We provide the [`icecore-standard`]() implementation. An icecore library can be used like any other C-library, but is meant to be used from ice control languages which provide a proper typesystem to guarantee type safety.

### ice control languages
The first ice control language is PureScript, with a dedicated [PureIce]() backend. A dependently typed ice control language is planned based on [Kami](). Dev toolchain developers write their glue code in a control language, and their individual transformation steps as ICE-functions.

### ICE-type providers
ICE is agnostic over the runtime representation of data. This means that various language runtimes and binary representation formats can coexist in one dev toolchain. The support for various data type representations is given by ICE-type provider plugins, such as [`haskell-ice-types`]() and [`rust-ice-types`](). Such plugins can be loaded dynamically at runtime if they are required.

### ICE-functions
The main purpose of ICE is to be an environment in which ICE-functions, i.e., the various computation or transformation steps of your toolchain can be run. You can use any language to write ICE-functions, as long as a supporting ICE-type provider exists.

### Rei buildsystem and generic language frontend
Usually language toolchains follow a similar general pattern, [Rei]() is a framework written in PureIce, catering to this standard use case. This means that with Rei, you can get a language toolchain up and running simply by passing it ICE-functions for pipeline steps such as typechecking and compilation, everything else such as package management will use standard defaults.

## Toolchains using ICE
Currently the following projects are planned to run on ICE:
 - [Rei]()
 - [Kami]()
 - [A package manager for Agda]()

