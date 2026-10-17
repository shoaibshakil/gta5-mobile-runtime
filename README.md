# Los Santos Mobile Runtime (GTA V Android WebPort — Compressed Edition)

[![Platform](https://img.shields.io/badge/Platform-Android%2010%2B-green.svg)](https://android.com)
[![Architecture](https://img.shields.io/badge/Architecture-ARM64--v8a-blue.svg)](https://arm.com)
[![Graphics API](https://img.shields.io/badge/Graphics-Vulkan%20%2F%20WebGPU-red.svg)](https://vulkan.org)
[![GPU Target](https://img.shields.io/badge/GPU-Mali%20%26%20Adreno-orange.svg)](https://arm.com/products/silicon-ip-cpu)
[![Multiplayer](https://img.shields.io/badge/Multiplayer-UDP%20Peer%20Relay-brightgreen.svg)]()

An ultra-optimized, high-performance runtime for running Grand Theft Auto V assets on **ARM64 Android devices** using Cranelift JIT compilation, WebAssembly, and native Vulkan/WebGPU acceleration. 

Specifically fine-tuned for **MediaTek (Helio G & Dimensity)** and **Snapdragon** devices to prevent out-of-memory allocation crashes and thermal throttling while preserving crisp HD visual fidelity.

---

## ⚡ What Makes This Version Special?

Standard GTA V requires over 100 GB of storage and 8+ GB of VRAM. This specialized mobile port features:

- 📦 **Ultra-Compressed Game Footprint**: Stripped of redundant filler and multi-language audio packs down to **~10 GB total package size** (saving over 85 GB of storage).
- 🧠 **Anti-Crash Scudo Memory Guard**: Re-engineered Depth and Framebuffer allocations to stay strictly within Android's 256 MB allocator ceiling.
- ⏱️ **Extended Session Stability**: Disabled background gameplay replay recording buffers (`-noreplay`) and implemented active cache eviction (`maxFileStoreSize: 8192`), eliminating the 4.5 GB RAM memory leak for uninterrupted long gameplay.
- 🎮 **Peer-to-Peer Local Multiplayer**: Built-in zero-latency UDP networking allowing multiple players to explore Los Santos together over a local Hotspot or Wi-Fi network.
- 🎨 **Adaptive HD Graphics Pipeline**: Built-in FXAA Anti-Aliasing, 2× Anisotropic Texture Filtering, and responsive Level-of-Detail (LOD) geometry scaling.
- 🚀 **Universal MediaTek Auto-Tuner**: Includes `mediatek_universal_optimizer.py` to auto-calibrate settings for Helio G70/G80/G85/G88/G95/G99 and Dimensity chips.

---

## 📱 Hardware Requirements

| Component | Minimum | Recommended |
| :--- | :--- | :--- |
| **OS** | Android 10.0 or higher | Android 12 / 13 / 14 |
| **SoC / Chipset** | MediaTek Helio G80 / Snapdragon 680 | MediaTek Helio G99 / Dimensity 700+ / Snapdragon 778G+ |
| **GPU** | ARM Mali-G52 / Adreno 610 | ARM Mali-G57, G68, G77 / Adreno 642L+ |
| **RAM** | 4 GB Physical RAM + Virtual zRAM | 6 GB – 8 GB Physical RAM |
| **Storage** | 15 GB free internal storage | 25 GB free internal storage |

---

## 📥 Download & Private Community

> [!IMPORTANT]
> **Legal Notice**: This repository hosts **ONLY** the open-source launcher, compatibility layer, and optimization scripts. It does **NOT** host or distribute copyrighted Rockstar Games `.rpf` asset archives.
>
> To access the pre-compressed 10 GB asset package (`game-import.zip`) and private Google Drive mirrors, join our **Private Telegram Community**:

👉 **[Join Private Telegram Channel](https://t.me/+BJNsRLeI77g0ZTM1)**

---

## 🚀 Installation & First Launch

1. **Install the APK**:
   - Download the APK from the [Releases](../../releases) tab or the private Telegram channel.
   - Install `GTA5_WEB_MALI.apk` on your device.
2. **Download the Game Data**:
   - Download `game-import.zip` (~10 GB) from the private Google Drive link in our Telegram channel.
   - Place `game-import.zip` into your phone's **Downloads** folder (`/sdcard/Download/`).
3. **Import Data**:
   - Open the **GTA 5** app.
   - Tap **"Import game ZIP"** and select `game-import.zip`.
   - The app will extract the assets into private storage (takes 3–5 minutes).
4. **First Compilation**:
   - Tap **"Play (wasmtime engine)"**.
   - On the very first launch, the Cranelift compiler converts `game.wasm` into a native ARM64 binary (`game.cwasm`). This takes 1–3 minutes. Future launches start instantly!

---

## 👥 How to Play Multiplayer with Friends

No internet connection or data usage required! Works seamlessly via direct phone-to-phone Hotspot:

```
[HOST PHONE]                                         [JOINING FRIEND]
Personal Hotspot: ON                                 Connect to Host's Wi-Fi Hotspot
Host Session: [✔] ON                                 Host Session: [ ] OFF
Server IP: 0.0.0.0                                   Server IP: 192.168.43.1
     │                                                    │
     └────────────────── UDP Port 6672 ───────────────────┘
```

1. **Create Connection**:
   - Turn **ON** **Personal Hotspot** on the Host phone.
   - Connect your friend's phone to your Wi-Fi Hotspot.
2. **Host Setup**:
   - Check **Multiplayer (Muguet UDP)**: `ON`
   - Check **Host a session**: `ON`
   - Enter your Player Name and tap **Play**.
3. **Friend Setup**:
   - Check **Multiplayer (Muguet UDP)**: `ON`
   - Uncheck **Host a session**: `OFF`
   - In **Server address**, enter: `192.168.43.1` (Android Hotspot gateway)
   - Enter Player Name and tap **Play**.
4. Both players will sync into the same Los Santos session with synchronized player coordinates, vehicles, and world physics!

---

## 🎨 Graphics Quality & Resolution Presets

In the app launcher screen, you can adjust the **"Render scale"** value to match your desired performance and visual target:

| Quality Preset | Render Scale Value | Internal Resolution | Target FPS | Best For |
| :--- | :---: | :---: | :---: | :--- |
| **480p (Performance)** | **`0.50`** | `800 × 360` | 30 FPS Rock Solid | 3 GB – 4 GB Budget Phones |
| **540p (Balanced)** | **`0.65`** | `1040 × 468` | 30 FPS Stable | Battery Saving & Cool Temps |
| **720p (HD Native)** | **`0.70` – `0.85`** | `1360 × 612` | 30 FPS | **Crisp, sharp visuals (Recommended)** |
| **1080p (Ultra Sharp)** | **`1.00`** | `1600 × 720` | 25 – 30 FPS | High-End Dimensity / Snapdragon |

---

## 🛠️ Universal MediaTek One-Click Optimizer

If you are experiencing stuttering on a MediaTek device, connect your phone to a PC via USB (with USB Debugging enabled) and run:

```bash
python mediatek_universal_optimizer.py
```

This tool automatically queries `/proc/meminfo` and `getprop`, detects your SoC tier, and configures the optimal RAM heap budget, LOD bias, and Mali rendering flags.

---

## 🔮 Future Roadmap

- [ ] **Dual-Mode Touch Controller**: Interactive top toggle button to switch seamlessly between **Walking Controls** (360° joystick, aim, punch) and **Driving Controls** (left/right steer buttons, gas, brake, handbrake).
- [ ] **Dedicated Online 4G/5G Relay Servers**: Play over mobile data across different cities without local hotspots.
- [ ] **Street & Stunt Racing Gamemodes**: Glowing 3D checkpoints, countdown start grids, and race lap timers.
- [ ] **Vehicle & Weapon Spawner Menu**: Quick in-game touch menu to spawn sports cars, bikes, and weapons.

---

## ⚖️ Legal Disclaimer

This project is an experimental, non-commercial research compatibility layer and launcher created for educational purposes. 

- This repository does **NOT** contain, redistribute, or reverse-engineer proprietary binary code or copyrighted asset files (audio, models, textures, or `.rpf` archives) owned by **Rockstar Games** or **Take-Two Interactive**.
- All game trademarks, logos, and character names are the registered intellectual property of Rockstar Games and Take-Two Interactive.
- Users must extract and utilize their own legitimate game archives.
