# OpenSimSearch

Allows in-world search for OpenSimulator: places, land for sale, events and classifieds. A region module (this DLL), and the web API service it queries (third-party helpers, see below).

A fork of [kcozens/OpenSimSearch](https://github.com/kcozens/OpenSimSearch), the one the [OpenSimulator wiki](http://opensimulator.org/wiki/OpenSimSearch) points to. Same source, with builds for recent versions of OpenSimulator. The original instructions are in [README](README), the origin and the license in [NOTICE](NOTICE) and [LICENSE](LICENSE).

## DLL binaries

A DLL binary only works with the version it was built for. Most recent versions are available as files of the [releases](https://github.com/GuduleLapointe/OpenSimSearch/releases).

- [0.9.3.x](https://github.com/GuduleLapointe/OpenSimSearch/releases/tag/0.4%2Bgit20261005.d81ecde) Oct. 05 2026
- [0.9.2.x](https://github.com/GuduleLapointe/OpenSimSearch/releases/tag/0.4%2Bgit20210131.67644ca) Jan. 31 2021
- [0.9.1.x](https://github.com/GuduleLapointe/OpenSimSearch/releases/tag/0.4%2Bgit20180713.1612abd) Jul. 13 2018

> Tip: a `MissingMethodException` at the first search means the dll was built for another one.

## Installation

1. **OpenSim**: copy the matching DLL in your opensim `bin/` folder, as `OpenSimSearch.Modules.dll`, adjust the configuration file and restart each simulator:

```ini
; OpenSim.ini
[Search]
  Module = OpenSimSearch
  SearchURL = "https://www.yourgrid.org/helpers/query.php"

[DataSnapshot]
  index_sims = true
  gridname = "Speculoos World"
  DATA_SRV_YourGrid = "https://www.yourgrid.org/helpers/register.php"
  ;; You can register on several directories:
  ; DATA_SRV_2do = "http://2do.directory/helpers/register.php"
  ; DATA_SRV_OtherEngine = "http://example.org/register.php"
```

> **Note**: the similarly named parameter in Robust.ini has **a different function**; ignore it or set it to the web search URL if this feature is provided by the helpers (this feature is purely web, it is not part of the DLL).

```ini
; Robust.ini
[LoginService]
  ; SearchURL = https://example.org/search/
[GridInfoService]
  ; search = https://example.org/search/
```

2. Install helpers on a web server. E.g.:

- [GuduleLapointe/opensim-helpers](https://github.com/GuduleLapointe/opensim-helpers)
- [GuduleLapointe/w4os](https://github.com/GuduleLapointe/w4os) ([WordPress plugin](https://wordpress.org/plugins/w4os-opensimulator-web-interface/))
- [MTSGJ/opensim.helper](https://github.com/MTSGJ/opensim.helper)
- the original webroot in this repository is deprecated and will be removed in the future

See [http://opensimulator.org/wiki/Webinterface](http://opensimulator.org/wiki/Webinterface) for more.

## Build from sources

- Fetch the source of the OpenSimulator version (not its binary release)
- copy the `OpenSimSearch/` folder to `OpenSim/addon-modules/`,
- execute:

```bash
./runprebuild.sh
dotnet build --configuration Release OpenSim.sln
```

The DLL is `bin/OpenSimSearch.Modules.dll`.
