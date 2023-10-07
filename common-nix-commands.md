
# Dealing with Haskell.nix

To see the derivation of the devShell for a haskell.nix flake, do:
```
nix eval .#devShell.<system>.drvPath
```
Where `<system>` is e.g. `"x86_64-linux"`.


To get the direct build time dependencies, you can do for example:
```
nix path-info --json --derivation /nix/store/m7s2mxzjbackgby27m6sx1cc9hc8flpd-ghc-shell-for-AgdaEval.drv
```

