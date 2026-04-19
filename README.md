# etlserver-build

Automated GitHub Actions build that combines the latest
[ET:Legacy](https://www.etlegacy.com/) Linux i386 server with the original
Enemy Territory 2.60b game files, producing a single archive ready for use
with [LinuxGSM etlserver](https://linuxgsm.com/servers/etlserver/).

## Why this exists

ET:Legacy requires both its own server binary **and** the original Enemy
Territory pak files (`pak0.pk3`, `pak1.pk3`, `pak2.pk3`) to run.  LinuxGSM
currently ships an i386 combined package, but this repo automates keeping it
up to date with the latest ET:Legacy release.

## What the workflow does

1. Scrapes `https://www.etlegacy.com/download` to find the latest stable
   Linux i386 archive URL.
2. Checks whether a release already exists for that version — skips the build
   if it does.
3. Downloads the ETL Linux x86_64 archive and the Enemy Territory 2.60b files.
4. Renames `etlded.i386` → `etlded` for LinuxGSM compatibility.
5. Merges the original ET `pak*.pk3` files into `etmain/`.
6. Packages everything into a flat `etlegacy-vX.Y.Z-i386-et-260b.tar.xz`
   archive and publishes a GitHub Release.

## Schedule

The workflow runs every **Monday at 02:00 UTC** and can also be triggered
manually via `workflow_dispatch`.
