# Ciel-Layman (Early WIP)

## Introduction

Ciel-Layman is similar to Layman from Gentoo, but it is designed for AOSC OS, whose packaging toolkit consists of ACBS and Ciel.

Ciel-Layman allows a user to apply user-defiend patches to the TREE, before Ciel starts building.

## Overlay Management

An overlay is a git repository which contains patches for packages.

A user maintains a mappting table from PackageName to Array\<Overlay>. For each Overlay being enabled on a Package, its patches for the package are applied into the TREE.

Ciel-Layman maintains an internal list of overlays. The user may maintain a separate list of alternative overlays.

For more information, see `docs/Overlay.md`.

## Usage

### Commands

| Subcommand                   | Description                                                                  |
| ---------------------------- | ---------------------------------------------------------------------------- |
| `lsall`                      | Print list of known overlays.                                                |
| `clone REPO1,REPO2`          | Clone selected overlays to local machine.                                    |
| `rm REPO1,REPO2`             | Remove overlays from local machine.                                          |
| `ls`                         | Print list of cloned overlays.                                               |
| `sync`                       | Pull all overlays.                                                           |
| `sync REPO1,REPO2,REPO3`     | Pull selected overlays, delimited by comma.                                  |
| `which PKG_NAME`             | Get a list of overlays which have patches for a package.                     |
| `use PKG_NAME REPO1,REPO2`   | Register overlays for a package.                                             |
| `unuse PKG_NAME REPO1,REPO2` | Un-register overlays for a package.                                          |
| `perpare PKG_NAME`           | Apply patches for a package from overlays into the TREE.                     |
| `test PKG_NAME`              | Test if there is any conflict for the package among its registered overlays. |
| `stash`                      | Run `git stash` in the TREE.                                                 |

Notes:

- `PKG_NAME` should contain category prefix.

### Conditions

Ciel-Layman works with the following assumptions:

- The directory `/var/cielroot-layman` is a Ciel workspace root.
- There is already a Ciel instance named `ciel-layman-main`.
- Before building any package (with overlay patches), you have already installed it in APT.

These assumptions can be removed in future, probably!

### Copyright

Copyright (c) 2021 Neruthes.

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License along
with this program; if not, write to the Free Software Foundation, Inc.,
51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.