# Overlay Management

## Abstract

An overlay is a git repository which contains patches for packages.

A user maintains a mappting table from PackageName to Array\<Overlay>. For each Overlay being enabled on a Package, its patches for the package are applied into the TREE.

Ciel-layman maintains an internal list of overlays. The user may maintain a separate list of alternative overlays.





## Maintaining An Overlay

### Structure

An overlay repository shall have the following structure:

```
example-overlay-repo
|-- Manifest.json
`-- extra-vcs
    `-- git
        |-- patches
        |   `-- 0003-some-patch.patch
        `-- spec
```

### Manifest

A Manifest is a JSON file which contains certain configutations.

```json
{
    "name": "Neruthes",
    "maintainers": "Neruthes",
    "syncType": "git",
    "syncUri": "https://github.com/neruthes/AOSC-overlay-neruthes",
    "homepage": "https://github.com/neruthes/AOSC-overlay-neruthes",
    "description": "Personal overlay, maintained by Neruthes."
}
```

| Field         | Description                                                      |
| ------------- | ---------------------------------------------------------------- |
| `name`        | The name of this overlay.                                        |
| `maintainers` | The maintainers of this overlay. A list delimited by comma. |
| `syncType`    | Now only `git` is supported. Will probably support `rsync`.      |
| `syncUri`     | The URI for synchronization.                                     |
| `homepage`    | Where people read README.                                        |
| `description` | A brief description to explain its reason of existence.          |


### Spec

Each package should contain the spec, which should be exactly the same with the corresponding spec in the TREE.
Ciel-Layman checks the sha256sum of the two spec files;
if the sha256sum results do not match, Ciel-Layman will refuse to apply an overlay to the package when preparing.
This frees the user from worrying about version mismatch.

The user may bypass this check by putting the overlay name in `/etc/ciel-layman/bypass-version-check`.


## Local Files

Ciel-Layman puts all overlays in `/var/db/ciel-layman-overlays`; the overlay name is used as the name (case-sensitive) of the directory.

The user may maintain custom overlays here as well, as long as names do not collide with
distro-managed ones (names listed in `/etc/ciel-layman/distro-overlays`).

This implies that the user may clone "wild" overlays in `/var/db/ciel-layman-overlays`.
Ciel-Layman treats "verified" overlays and "wild" overlays equally (in most scenarios).
Ciel-Layman does not support cloning "wild" overlays, because any user with this need should be skilled enough to manually execute `git clone`.

Ciel-Layman maintains a list of cloned overlays at `/etc/ciel-layman/cloned-overlays`, as a plaintext file with each name in a line.
To successfully clone an overlay repo, the directory shall not exist, and this list shall not contain its name.

