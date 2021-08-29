# Overlay Management

## Abstract

An overlay is a git repository which contains patches for packages.

A user maintains a mappting table from PackageName to Array\<Overlay>. For each Overlay being enabled on a Package, its patches for the package are applied into the TREE.

Ciel-layman maintains an internal list of overlays. The user may maintain a separate list of alternative overlays.

## Maintaining An Overlay

### Structure

An overlay repository shall have the following structure:

```
example-overlay-repo/
├── Manifest
└── extra-vcs
    └── git
        └── patches
            └── 0003-some-patch.patch
```

### Manifest

A Manifest is a JSON file which contains certain configutations.

```
{
    "name": "Neruthes",
    "maintainers": "Neruthes",
    "syncType": "git",
    "syncUri": "https://github.com/neruthes/AOSC-overlay-neruthes",
    "homepage": "https://github.com/neruthes/AOSC-overlay-neruthes",
    "description": "Personal overlay, maintained by Neruthes."
}
```