# Configuration

## Global Configuration

Config file path: `/etc/ciel-layman/config`.

The file format should look like:

```
key_1=value_1
key_2=value_2
```

The following options are applicable:

| Option           | Values         | Description                                                                                       |
| ---------------- | -------------- | ------------------------------------------------------------------------------------------------- |
| localRepoEnabled | `true` `false` | Consider `/usr/local/ciel-layman-localrepo` as a local overlay repo, using reserved name `LOCAL`. |
| localRepoAlways  | `true` `false` | Always apply all patches in LOCAL without checking whether a package uses it.                     |
| safeRemoval      | `true` `false` | When removing overlay, fail if any package uses it.                                               |

## Distro Configuration

The distro maintainers shall maintain an array of manifests of "verified" overlays at `/etc/ciel-layman/distro-overlays-dict.json`, which looks like:

```json
{
    "Neruthes": {
        "name": "Neruthes",
        "maintainers": "Neruthes",
        "syncType": "git",
        "syncUri": "https://github.com/neruthes/AOSC-overlay-neruthes",
        "homepage": "https://github.com/neruthes/AOSC-overlay-neruthes",
        "description": "Personal overlay, maintained by Neruthes."
    },
    "example": {
        "name": "example",
        "maintainers": "AOSC-Developers",
        "syncType": "git",
        "syncUri": "https://github.com/AOSC-Dev/overlay-example",
        "homepage": "https://github.com/AOSC-Dev/overlay-example",
        "description": "Example overlay."
    }
}
```

Also, the distro maintainers shall maintain a script at `/etc/ciel-layman/distro-fetch-list.sh`,
which will be executed by Ciel-Layman when the user executes `ciel-layman fetch`.
This file can be a simple script `exit 1`; Exit code 1 means that the distro does not officially support Ciel-Layman.