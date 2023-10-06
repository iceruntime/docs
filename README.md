# Documentation for the ICE-runtime

## What?
A language & runtime for package managers and compiler front-ends. Caching & package-management is delegated to Nix.

## Why?
Nix does not integrate well with language-specific buildsystems: cargo, cabal, etc. It would be best if these buildsystems
used Nix under the hood, but this is of course quite difficult to realize for existing buildsystems. We aim to make it easy
to write buildsystems (and package-managers based on Nix). This way, future languages can profit easily from a direct Nix integration!

Current problems with Nix-buildsystem integrations:
 - [Cargo does not provide access to its dependency resolution algorithm](https://hadean.com/blog/managing-rust-dependencies-with-nix-part-i/)
 
