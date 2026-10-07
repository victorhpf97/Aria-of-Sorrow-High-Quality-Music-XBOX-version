# 🎮 Castlevania: Aria of Sorrow — High Quality Music for Xbox

This folder contains the **Xbox Series X/S RetroArch version** of the Aria of Sorrow High Quality Music project.

> ⚠️ This version is intended for **RetroArch running in Xbox Dev Mode**.

The modified mGBA core replaces Aria of Sorrow's original background music with external WAV files while keeping the original game sound effects.

---

## 🎬 Video Demo

[![Watch the Aria of Sorrow HQ Music Mod](https://img.youtube.com/vi/Dm6gLcpuvKk/maxresdefault.jpg)](https://youtu.be/Dm6gLcpuvKk)

## ⚠️ Important: the Xbox core must be installed

On Xbox, do **not** try to use the custom DLL directly from the USB drive as if it were a normal playlist core.

The custom mGBA core must first be installed through RetroArch.

### Install the core

1. Copy the custom Xbox core DLL to your USB drive.
2. Open RetroArch on Xbox.
3. Go to:

```text
Load Core
→ Install or Restore a Core
```

4. Browse to the custom core DLL on the USB drive.
5. Select it and let RetroArch install the core.
6. After installation, load the installed custom mGBA core from RetroArch.

If the release includes a matching `.info` file, keep its base filename identical to the DLL.

Example:

```text
mgba_victor_dev_libretro.dll
mgba_victor_dev_libretro.info
```

---

# 📁 Music folder on Xbox

The current Xbox build uses this path in the source code:

```c
#define ARIA_MUSIC_DIR "E:/RetroArch/MOD/Aria of sorrow"
```

This means the music files must be located at:

```text
E:/RetroArch/MOD/Aria of sorrow/
```

Example:

```text
E:/
└── RetroArch/
    └── MOD/
        └── Aria of sorrow/
            ├── 1.wav
            ├── 2.wav
            ├── 3.wav
            ├── 4.wav
            └── ...
```

## 💾 What does `E:` mean?

`E:` is the drive letter that **the Xbox assigns to the USB drive**.

It does **not** matter which drive letter the same USB uses on your Windows PC.

For example, your USB could appear on your PC as:

```text
D:
```

but when RetroArch runs on Xbox it may appear as:

```text
E:
```

The current Xbox build expects the USB to be available to RetroArch as:

```text
E:
```

So the complete path expected by the core is:

```text
E:/RetroArch/MOD/Aria of sorrow/
```

> ⚠️ If your Xbox/RetroArch exposes the USB using a different drive letter, this build will not find the music. The `ARIA_MUSIC_DIR` path would need to be changed in the source and the Xbox core rebuilt.

---

# 🎵 Adding replacement music

Each replacement song uses the numeric ID of the original Aria of Sorrow track.

Example:

```text
1.wav
2.wav
3.wav
...
45.wav
```

For example:

```text
2.wav  = Ruined Castle Corridor
5.wav  = Dance Hall
18.wav = Final Decisive Battle
```

You can replace only the songs you want.

If a compatible WAV file exists for a song ID, the custom track is played.

If it does not exist, the original GBA music continues to play.

---

# 🎧 Required WAV format

The replacement audio must use:

```text
Format: WAV
Codec: PCM signed 16-bit
Sample rate: 32768 Hz
Channels: Mono or Stereo
```

---

# 🔄 Converting music with FFmpeg

On Windows, install FFmpeg with PowerShell:

```powershell
winget install Gyan.FFmpeg
```

Then put your WAV files in a folder and run:

```powershell
mkdir convertido -ErrorAction SilentlyContinue

Get-ChildItem *.wav | ForEach-Object {
    ffmpeg -y -i $_.FullName -ar 32768 -c:a pcm_s16le ("convertido\" + $_.Name)
}
```

The converted files will be placed in:

```text
convertido/
```

Rename them according to the game's music ID:

```text
2.wav
5.wav
18.wav
```

Then copy them to:

```text
E:/RetroArch/MOD/Aria of sorrow/
```

---

# ✅ Example Xbox setup

Your USB can look like this:

```text
E:/
└── RetroArch/
    ├── roms/
    │   └── GBA/
    │       └── Castlevania - Aria of Sorrow (USA).gba
    │
    └── MOD/
        └── Aria of sorrow/
            ├── 1.wav
            ├── 2.wav
            ├── 3.wav
            └── ...
```

The custom core itself is installed into RetroArch using:

```text
Load Core
→ Install or Restore a Core
```

After that:

1. Load the installed custom mGBA core.
2. Open Castlevania: Aria of Sorrow.
3. The core reads the current in-game music ID.
4. If a matching WAV exists in the Xbox music folder, it replaces that song.
5. Game sound effects continue normally.

---

## 🎼 Music IDs

Use the same music ID / set list documented in the main project README.

Examples:

| ID | Track |
|---:|---|
| 1 | Clock Tower |
| 2 | Ruined Castle Corridor |
| 3 | Underground Reservoir |
| 4 | Demon Castle Top Floor |
| 5 | Dance Hall |
| 6 | Phantom Palace |
| 7 | Demon Castle Study |
| 8 | Chapel |
| 9 | Forgotten Garden |
| 10 | The Purgatory Arena |
| 11 | Sacred Cave |
| 12 | Chaotic Realm |
| 18 | Final Decisive Battle |
| 19 | Battle for the Throne |
| 31 | Battle Against Chaos |
| 38 | Outdoor / Ambient 2 — Wind outside |

See the main `README.md` for the complete mapping from `1` to `45`.

---

## 📦 ROM and music files

This project does **not** include:

- Castlevania: Aria of Sorrow ROM files
- Nintendo BIOS files
- Commercial soundtrack files
- Third-party copyrighted music

Use your own legally obtained game and audio files.

---

## 🛠️ Current Xbox limitation

The Windows version can automatically determine its RetroArch installation path.

The current Xbox version instead uses a fixed music path:

```c
#define ARIA_MUSIC_DIR "E:/RetroArch/MOD/Aria of sorrow"
```

This is intentional for the current Xbox build because the installed UWP core and the external USB storage are located in different places.

A future version may improve Xbox path detection.

---

## ❤️ Project goal

The goal is to keep Aria of Sorrow's gameplay and original sound effects intact while allowing its soundtrack to be replaced with high-quality arrangements, covers, remasters, or your own custom music.

You can replace one song or the entire soundtrack.
