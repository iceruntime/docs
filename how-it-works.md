# How it works

There are the following components:
 - icecore-interface (a formal specification of the interface
   that an icecorelib has to expose)
    - package management
    - caching
    - incremental computation
    - type provider plugins
    - function plugins
 - beam-icecorelib
    - an implementation of the icecore-interface with the BEAM virtual machine (erlang, elixir)
 - purescript-on-ice
    - exposing the icecorelib to purescript
    - in the best case this can take any icecore-interface implementation
 - a future higher level language which embeds an icecore-interface



