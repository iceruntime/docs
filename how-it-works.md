# How it works

There are the following components:
 - ice-core-interface (a formal specification of the interface
   that an ice-corelib has to expose)
    - package management
    - caching
    - incremental computation
 - beam-ice-corelib
    - an implementation of the ice-core-interface with the BEAM virtual machine (erlang, elixir)
 - purescript-on-ice
    - exposing the ice-corelib to purescript
    - in the best case this can take any ice-core-interface implementation
 - a future higher level language which embeds an ice-core-interface



