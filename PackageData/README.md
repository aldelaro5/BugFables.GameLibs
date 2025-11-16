# BugFables.GameLibs
This package includes publicized assemblies for use when compiling mods for the game Bug Fables.

Specifically, it includes the following:

- All the UnityEngine assemblies included with the game. They are publicized, but not stripped as they are public redistributable assemblies. They match the assemblies any Mono compiled game using Unity version 2018.4.12f1 would ship with.
- The Bug Fables specific assembly named Assembly-CSharp.dll. Since all of its content is subject to copyrights and normally requires a purchase of the game to access it, the assembly is publicized, but stripped meaning only type signatures are included in this assembly. It is the bare minimum needed to compile a mod. You must purchase a copy of the game to have an unstripped version of this assembly.

## Purpose of these assemblies
The purpose of these assemblies is to avoid the need for reflection when accessing anything speakable, but non-public which is not only more convenient, but also faster. It also eliminates the need to explicitly reference these assemblies from the copy of the game which isn't version control friendly.

## Accessibility checks are runtime
In order to access anything that was originally non-public at runtime as a result of referencing these assemblies in your mod, you MUST set the `AllowUnsafeBlocks` property in your csproj to `true`. This is required by Mono to disable the runtime visibility checks at runtime, even if you are not actually using any `unsafe` code.

## Versioning
This package uses a versioning scheme that loosely follows the game's versioning scheme. It allows to target any past versions of the game even if the publicized API of the assembly changed. This is done by selecting the version that matches the game version.

Each version is in the format Major.Minor.Patch. Here are their semantics for this package:

- Major: The advertised game version without any dots in the lower left corner of the title screen. NOTE: This is NOT the version contained in the version.txt file of the game. Example: 113 means game version 1.1.3 while 102 means game version 1.0.2
- Minor: A number that increments for each time the same game version was published, but with changes that impacts the publicized API. See the section below for the detailed mappings
- Patch: A number reserved to version this package. Should there be an update to the way the assemblies are published in this package, this number will increment. It means that for a given Major.Minor combination, the latest version will have the highest patch version number

Additionally, versions 113.1.0 and later only supports net472 targeting because the second release of the game version 1.1.3 marks the switch to the new net472 Mono runtime. Older versions dual targets net35 and net472 because it is possible on these older versions to upgrade the Mono runtime to the new one so it allows to target with or without Mono upgrade.

## Detailed mappings
Here are the detailed game version updates to this package's Major.Minor combinations:

- 1.0.0 -> 100.0
- 1.0.1 -> 101.0 (this version was published twice, but both of them have the same publicized API)
- 1.0.2 -> 102.0
- 1.0.3 -> 103.0 (the first update that was released on 2019-12-14)
- 1.0.3 -> 103.1 (the second update that was released on 2019-12-14)
- 1.0.3 -> 103.2 (the first update that was released on 2019-12-15)
- 1.0.3b -> 103.3 (the second update that was released on 2019-12-15)
- 1.0.3c -> 103.4
- 1.0.3d -> 103.5
- 1.0.4 -> 104.0 (the first update that was released on 2020-01-02)
- 1.0.4 -> 104.1 (the second update that was released on 2020-01-02 and also the update released on 2020-01-06)
- 1.0.5 -> 105.0 (the update released on 2020-01-19)
- 1.0.5 -> 105.1 (the update released on 2020-02-07)
- 1.1.0 -> 110.0
- 1.1.1 -> 111.0
- 1.1.2 -> 112.0
- 1.1.3 -> 113.0 (last version published with net35 Mono shipped by default on 2024-05-29)
- 1.1.3 -> 113.1 (first version published with net472 Mono on 2024-05-29)
- 1.2.0 -> 120.0

## Note about originally non-public types and members
Any type or member that was originally non-public is denoted by an `OriginalAttribute` with the original visibility.
