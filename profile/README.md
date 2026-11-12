# OBS Stream Music Viewer (OSMV)

![Status](https://img.shields.io/badge/status-working-success)
![Version](https://img.shields.io/badge/version-5.1.0-blue)
![Platform Windows](https://img.shields.io/badge/platform-Windows%2010%2F11-blue)
![Platform Linux](https://img.shields.io/badge/platform-Linux-orange)
![C++20](https://img.shields.io/badge/Language-C%2B%2B20-00599C)
![GUI](https://img.shields.io/badge/GUI-Dear%20ImGui-blueviolet)

Welcome to the **StreamMusicViewer** organization! **OSMV v5.1.0** is an ultra-lightweight native **C++20** companion suite for OBS Studio and Discord Rich Presence. Rewritten from the ground up with **Dear ImGui** and a dual-process architecture, it combines real-time music overlays with Snaz-inspired streaming tools while keeping background RAM around **4.5 to 6 MB**.

## Features

- **Now Playing (OBS Overlay Studio + Snaz exports)** — Detects active media every second via WinRT SMTC (Windows) and D-Bus MPRIS (Linux), exports `shared/current_song.json` / `.js` and `shared/widget_config.json` / `.js`, and optionally outputs `TrackArtist.txt`, `TrackSong.txt`, `TrackAlbum.txt`, `PlayingNow.txt`, and `track-info.json`.
- **OBS Overlay Studio & Live Previews** — 7 built-in presets, saved multi-scene presets (`?preset=<Name>`), custom typography/marquee/transitions, 3 dynamic cover-color modes, 5 audio visualizer styles, a syntax-highlighted CSS editor, and embedded + browser (`shared/preview.html`) previews.
- **Discord Rich Presence** — Native C++ Discord IPC client displaying a Listening activity (`type: 2`) with iTunes artwork lookup, album metadata, and status badges.
- **Time, Date & Timers** — Real-time `Time.txt`, localized `Date.txt`, target `Countdown.txt`, `ChronoDown.txt`, and `ChronoUp.txt` (`$totalminutes`).
- **System Info** — Lightweight native hardware telemetry (`$CPU_USAGE`, `$RAM_MB_AVAIL`, `$RAM_%_IN_USE`, `$RAM_%_AVAIL`, `$AMOUNT_PROCESSES`, `$UPLOAD`, `$DOWNLOAD`) written to `SystemInfo.txt`.
- **Textline Changer & Dynamic Files** — Rotates custom messages (`TextlineChanger.txt`) and periodically fetches remote HTTP/HTTPS text or image files for OBS.
- **Twitch Helix Integration** — Automatic localhost OAuth token capture, live viewer counts (`TwitchViewers.txt`), category search, and stream title/game updates with saved presets.
- **Dual-Process Low RAM** — Event-driven GUI (~51–58 MB on Windows) terminates completely on **Headless Mode** / close, leaving only the ~4.5–6 MB background daemon in the system tray.

## How It Works

```mermaid
graph TD
    A[Media / OS / HTTP / Twitch] -->|WinRT / MPRIS / Native APIs| B["OSMV Daemon (C++20)"]
    B -->|Local IPC| G["OSMV GUI (Dear ImGui, on demand)"]
    B -->|Writes JSON / JS| C["shared/current_song.* & widget_config.*"]
    B -->|Writes .txt / images| F[shared/dynamic_text/*]
    B -->|Native IPC| H[Discord Rich Presence]
    C -->|Loaded by| D[OBS Browser Source]
    F -->|Read by| E[OBS Text / Image Sources]
```

---

## Quick Start

### Windows

1. Go to the **[Releases](https://github.com/StreamMusicViewer/OSMV/releases)** page and download the latest `.zip` (or build from source with `windows\build.bat`).
2. Keep `OSMV.exe` alongside the `shared/` folder (`shared/index.html`, `shared/style.css`).
3. Run `OSMV.exe` (single standalone executable, no external DLLs required).
4. Configure OBS (see below).

### Linux

**Dependencies:** `dbus-1`, `libcurl`, `glfw3`, `OpenGL` (for `osmv-gui`; the `osmv` daemon requires only `dbus-1` and `libcurl`).

1. Go to the **[Releases](https://github.com/StreamMusicViewer/OSMV/releases)** page or build from source with `./linux/build.sh`.
2. Keep `osmv` and `osmv-gui` alongside the `shared/` folder.
3. `chmod +x osmv osmv-gui && ./osmv`
4. Configure OBS (see below).

---

## Configure OBS

1. **Music Widget (Default Style)**: Add a **Browser** source -> check **Local file** -> select `shared/index.html` -> set **Width: 600**, **Height: 200** (or test in `shared/preview.html` via **Browser Preview**).
2. **Multi-Scene Presets**: Save custom styles in **Now Playing -> Presets & Style**, click **Scene URL**, and paste `file:///.../shared/index.html?preset=<Name>` with **Local file** unchecked.
3. **Dynamic Text**: Add a **Text (GDI+)** (Windows) or **Text (FreeType 2)** (Linux) source -> check **Read from file** -> select any generated `.txt` file in `shared/dynamic_text/`.

*Close the configuration window anytime to enter Headless Mode while the daemon keeps running in the system tray.*

---

## Our Repositories

| Repository | Status | Description |
| :--- | :--- | :--- |
| **[OSMV](https://github.com/StreamMusicViewer/OSMV)** | Active (v5.1.0) | Native C++20 suite: Now Playing (OBS Overlay Studio), Discord RPC, Timers, System Info, Dynamic Files, Twitch Helix, and ultra-low RAM daemon. |
| **[OSMV Lite](https://github.com/StreamMusicViewer/OSMV-lite)** | Archived | Archived — superseded by OSMV v5.1.0, which offers all features while using even less RAM. |

---

## Links & Creator
- **Documentation:** [streammusicviewer.github.io/OSMV](https://streammusicviewer.github.io/OSMV/)
- **Creator:** [@Ulyxx3](https://github.com/Ulyxx3)
- **License:** [GPL-3.0](https://github.com/StreamMusicViewer/OSMV/blob/main/LICENSE)
- **Troubleshooting:** [Troubleshooting Guide](https://github.com/StreamMusicViewer/OSMV/blob/main/TROUBLESHOOTING.md)

---
*Built for streamers who care about every detail and every megabyte of their broadcast.*
