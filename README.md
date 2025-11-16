# BugFables.GameLibs
This repository contains all the scaffolding needed to build every version of the BugFables.GameLibs nuget packages. Only the binaries are given here since it's not really practical to automate the downloading of the game as it gets complicated copyright wise.

For details on usage, check the package [README](https://github.com/aldelaro5/BugFables.GameLibs/blob/master/PackageData/README.md)

All UnityEngine binaries are publicized, but not stripped while all versions of the game assembly are publicized AND stripped.

The publicizer used is [BepInEx.AssemblyPublicizer](https://github.com/BepInEx/BepInEx.AssemblyPublicizer) version 0.5.0-beta.2 with default settings for the UnityEngine assemblies and with --strip for the game assemblies.

All the original game assemblies were pulled using a Steam account owning the game and [DepotDownloader](https://github.com/SteamRE/DepotDownloader) to download every version of the game.
