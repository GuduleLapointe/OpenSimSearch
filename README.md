# OpenSimSearch

Search for OpenSimulator: places, land for sale, events and classifieds. A region module (the DLL), and the web service it queries (`webroot/`).

A fork of [kcozens/OpenSimSearch](https://github.com/kcozens/OpenSimSearch), the one the [OpenSimulator wiki](http://opensimulator.org/wiki/OpenSimSearch) points to. Same source, with builds for recent versions of OpenSimulator. The original instructions are in [README](README), the origin and the license in [NOTICE](NOTICE) and [LICENSE](LICENSE).

## Builds

The binaries are not in the repository, they are the files of the [releases](../../releases). A release is a snapshot of the sources, named `0.4+git<date>.<commit>` (0.4 is the version the module declares). Each file is built for one version of OpenSimulator: `OpenSimSearch.Modules-opensim-<version>.dll`, or `-unstable-<commit>` for a development build of OpenSimulator.

A DLL only works with the version it was built for: a `MissingMethodException` at the first search means it was built for another one. Each release says which versions a file was used with.

## Install

1. Copy the DLL of your OpenSimulator version to its `bin/` folder, as `OpenSimSearch.Modules.dll`.
2. In `OpenSim.ini`, `[Search]`: `Module = "OpenSimSearch"` and `SearchURL = "http://yourserver/search/query.php"`.
3. The web service: see [README](README). `webroot/` is kept as it was published; the web part of [opensim-helpers](https://github.com/GuduleLapointe/opensim-helpers) is more advanced, and this copy may be removed from here.

## Build it yourself

With the source of the OpenSimulator version (not its binary release): copy the `OpenSimSearch/` folder to `OpenSim/addon-modules/`, then `./runprebuild.sh` and `dotnet build --configuration Release OpenSim.sln`. The DLL is `bin/OpenSimSearch.Modules.dll`.

## Changes from kcozens' version

- `prebuild.xml` has no `frameworkVersion` and no `System` references, which only gave warnings with .NET 8 (the DLL is the same).
- `LICENSE`, `NOTICE` and this file.
