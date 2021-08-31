# Files

Ciel-Layman uses the following files to manage information.

Files may be managed by User, Distro, and Internal.




## User

Users are encouraged to edit these files. Post-install scripts may creates these files with default contents.

### /etc/ciel-layman/config

Basic configuration files.

### /etc/ciel-layman/bypass-version-check

A list of overlay names, delimited by LF.

If an overlay is included in this list, it will not be subject to version matching checks
when preparing patches for any package.





## Distro

Only the distro maintainers should manage these files.

### /etc/ciel-layman/distro-overlays

A list of overlay names, delimited by LF.

### /etc/ciel-layman/distro-overlays-dict.json

A dictionary of overlay specifications.

### /etc/ciel-layman/distro-fetch-list.sh

Script to fetch latest list of overlays.



## Internal

These files are managed by Ciel-Layman itself.

### /etc/ciel-layman/cloned-overlays

A list of overlay names, delimited by LF.

### /var/db/ciel-layman-overlays

Direcotry. Overlay repositories.

### /var/db/ciel-layman/package.use/PKGNAME

A list of overlays which are used for this package, delimited by LF.

### /var/db/ciel-layman/overlay.use/OVERLAYNAME

A list of packages which use this overlay, delimited by LF.




## Others

These files are related to Ciel-Layman, but are not exactly related.

### /var/cielroot-layman

Directory. Ciel workspace root.


