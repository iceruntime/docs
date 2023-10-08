# How it works

**NOTE**: This project is very early in its design phase and this document may change relatively frequently as we try to work out the best overall structure and tools/frameworks/languages that we want to use. Also keep in mind that this document is written in a way that suggests that ICE is already implemented, but at the moment this is just a glimpse into the future which we aim to bring about.

ICE is an infrastructure provider for language toolchains. Its core function is to provide primitives for [package management](), [caching]() and [incremental computation]() The idea is that with ICE, language designers can focus on the backend of their language while utilizing the power of ICE for easily dealing with frontend matters.

The benefits are threefold:
 - easy interop with other ICE-languages.
 - unification of developer tooling.
 - integration with the Nix ecosystem.

### Sounds good! How would I use ICE for my new language?

First, you have to make sure that there is a [typing provider plugin]() available for the language(s) you want to implement your new language in. Implement your backend pipeline steps such as module resolution, typechecking and compilation. Then compile them into a [function plugin]() which can be used from ICE. Finally, write the  code which glues all your pipeline steps together in one of the supported [ICE-languages]().

### What if I want to use ICE for my already existing language?

Theoretically, ICE is intended to be highly modular, but its features are still designed around it being the main entry point of a language toolchain. This means that to reap most of the benefits of the ICE ecosystem, you are going to have to use ICE as a thin layer around your toolchain. Alternatively, you could use ICE as a driver for a part of your pipeline.

Depending on your goals, various solutions are possible, contact us to discuss!

## Features

### Package management

### Parsing

### Strong static types

### Caching

### Incremental computation


## ICE ecosystem

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

### `icecore` interface

### `icecore` implementations

### `ice-plugins`

### `ice-languages`

#### PureScript

#### High level language
Possibly based on `kami`.

### `rei` buildsystem







