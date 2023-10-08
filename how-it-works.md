# How it works

**NOTE**: This project is very early in its design phase and this document may change relatively frequently as we try to work out the best overall structure and tools/frameworks/languages that we want to use.

ICE is an infrastructure provider for language toolchains. Its core function is to provide primitives for [package management](), [caching]() and [incremental computation]() The idea is that with ICE, language designers can focus on the backend of their language while utilizing the power of ICE for easily dealing with frontend matters.

The benefits are threefold:
 - easy interop with other ICE-languages.
 - unification of developer tooling.
 - integration with the Nix ecosystem.

### That sounds good! How can I use ICE for my language?

See here: considering haskell, bla bla IO and we are an alternative monad.


## Components

<!-- , all the while being agnostic over the implemention of the backend via [type provider plugins]() and [function plugins](). -->

There are the following components:
 - icecore-interface (a formal specification of the interface
   that an icecorelib has to expose)
 - beam-icecorelib
    - an implementation of the icecore-interface with the BEAM virtual machine (erlang, elixir)
 - purescript-on-ice
    - exposing the icecorelib to purescript
    - in the best case this can take any icecore-interface implementation
 - a future higher level language which embeds an icecore-interface


## Icecore-interface





