# OBS Stream Music Viewer (OSMV)

Welcome to the **StreamMusicViewer** organization! We build elegant, lightweight, and zero-dependency "Now Playing" widgets for OBS streamers.

Your Music. **On Stream.** Perfectly.

## What We Do
Our open-source tools allow you to seamlessly display your currently playing music—from Apple Music, Spotify, Chrome, Edge, and YouTube Music—directly on your stream. No complex setups, no background Python/Node.js servers, just a simple executable and a beautiful OBS Browser Source.

## Our Repositories

We maintain two primary versions of the widget to suit your stream's performance and aesthetic needs:

| Repository | Description | Best For |
| :--- | :--- | :--- |
| **[OSMV (Full)](https://github.com/StreamMusicViewer/OSMV)** | The complete experience. Includes album artwork (with the background color adapting to it, Discord Rich Presence, and an audio visualizer. | Streamers wanting a visually rich, feature-complete widget with album art. |
| **[OSMV Lite](https://github.com/StreamMusicViewer/OSMV-lite)** | The minimal version. low resource usage with essential core features for maximum broadcast performance. | Streamers who need the absolute lowest system overhead. |

## How It Works



Our widgets run entirely locally on your machine (Windows 10/11) using a highly efficient pipeline:

1. **Detection:** The standalone `.NET 8` executable uses the Windows `GlobalSystemMediaTransportControlsSessionManager` API to detect what's playing (even when minimized).
2. **JSON Bridge:** Track info and artwork (as base64) are saved to a local `current_song.json` file every second.
3. **Live Widget:** An `index.html` file loaded as an **OBS Browser Source** polls the JSON and renders a beautiful card on your stream with smooth fade transitions.

## Key Features
* **Zero Dependencies:** Download, double-click, and you're done. No installers required.
* **Universal Compatibility:** Works out-of-the-box with any app integrated with Windows Media Controls.
* **Fully Customizable:** Don't like the default look? Simply edit the `style.css` file to change colors, sizes, and fonts to match your specific overlay.
* **Open Source:** Free forever, licensed under MIT.

## Links & Creator
* **Creator:** [@Ulyxx3](https://github.com/Ulyxx3)
* **License:** MIT

---
*Built for streamers who care about every detail of their broadcast. If you have feature requests or run into bugs, feel free to open an issue in the respective repositories!*
