# Los Santos Mobile Runtime (GTA V Android WebPort — Compressed Edition)

[![Platform](https://img.shields.io/badge/Platform-Android%2010%2B-green.svg)](https://android.com)
[![Architecture](https://img.shields.io/badge/Architecture-ARM64--v8a-blue.svg)](https://arm.com)
[![Graphics API](https://img.shields.io/badge/Graphics-Vulkan%20%2F%20WebGPU-red.svg)](https://vulkan.org)
[![GPU Target](https://img.shields.io/badge/GPU-Mali%20%26%20Adreno-orange.svg)](https://arm.com/products/silicon-ip-cpu)
[![Multiplayer](https://img.shields.io/badge/Multiplayer-UDP%20Peer%20Relay-brightgreen.svg)]()
[![Version](https://img.shields.io/badge/Release-v1.3-blueviolet.svg)](https://github.com/shoaibshakil/gta5-mobile-runtime/releases)

An ultra-optimized, high-performance runtime for running Grand Theft Auto V assets on **ARM64 Android devices** using Cranelift JIT compilation, WebAssembly, and native Vulkan/WebGPU acceleration. 

Specifically fine-tuned for **MediaTek (Helio G & Dimensity)** and **Snapdragon** devices to prevent out-of-memory allocation crashes and thermal throttling while preserving crisp visual fidelity.

---

## 📊 Real-Device Benchmark & FPS Testing

Here are real tested performance figures from our current development test devices:

| Device | Specs / Chipset | RAM | Tested FPS Range | Current Status |
| :--- | :--- | :---: | :---: | :--- |
| **Poco X6 Pro** | MediaTek Dimensity 8300 Ultra (Mali-G615) | **8 GB** | **20 – 30+ FPS** | **Playable & Stable (20+ FPS stable with minor fluctuations during fast driving)** |
| **Vivo Y20G** | MediaTek Helio G80 (Mali-G52 MC2) | **6 GB** | **5 – 12 FPS** | Experimental (CPU-bound 32-bit WASM software emulation) |

> [!NOTE]
> **Performance & Framerate Notice**: Tested on the **Poco X6 Pro (8 GB RAM)**, the game delivers **20+ FPS stable** in sandbox free roam and vehicle travel with only minor fluctuations during intense scene transitions. Lower-end devices (Helio G80/G85) face heavy CPU bottlenecking. We are actively refining asset streaming to stabilize 30–60 FPS across more chipsets!

---

## ⚡ What’s New in v1.3?

* 🌐 **Full Working Local Multiplayer (UDP)**: Connect with friends seamlessly over the same Wi-Fi or mobile hotspot.
* 🔍 **Auto Wi-Fi IP Detection**: Launcher automatically queries and displays your device's active local IP address in cyan, with clear Host / Client step-by-step instructions.
* 🛡️ **Second Engine Crash Fix**: Fixed `UnsatisfiedLinkError` on the second engine button (`PLAY (SAFE OPTIMIZED ENGINE)`), safely launching the optimized Wasmtime engine without crashes.
* ⚡ **AMD FSR 1.0 (Edge-Adaptive CAS Sharpening)**: Added an in-launcher checkbox for FidelityFX Contrast Adaptive Sharpening to reconstruct sharp 1080p images from 360p/540p render scales.
* 🌫️ **Natural Fog Distance Culling (OKM-Engine Style)**: Dynamically limits render distances of high-memory distant props and building LODs past 90m to eliminate GPU lag in dense downtown areas.
* 🚙 **Driving Memory Crash & Lag Fix**: Re-tuned file streaming buffers to 64 MB (`maxFileStoreSize: 65536`) and removed conflicting negative LOD biases, completely stopping the 30 FPS -> 5-2 FPS drop and eliminating the 3.0 GB WASM memory ceiling crash during fast driving.
* 📱 **Scaleform DirectX 11 Fix**: Fixed the transparent minimap radar and invisible in-game cellphone overlay by ensuring proper DX11 render target pipeline bindings.
* 🔊 **Restored Core Audio (SFX)**: Vehicle engine revs, footsteps, gunshots, and collisions are unmuted, while missing radio stream threads remain silenced to prevent CPU audio spinlocks.

---

## 📦 What Makes This Version Special?

Standard GTA V requires over 100 GB of storage and 8+ GB of VRAM. This specialized mobile port features:

- 📦 **Ultra-Compressed Game Footprint**: Stripped of redundant filler and multi-language audio packs down to a lightweight portable package size (saving over 85 GB of storage).
- 🚦 **In-App Traffic & Pedestrian Switcher**: 
  - **Off (Maximum FPS / Zero Lag):** Eliminates ambient cars and ped AI load completely.
  - **Light (Anti-Lag & Cool Phone):** Only 2–3 ambient cars for smooth cruising without heating.
  - **Balanced & High:** Moderate to full city density.
- 🎮 **Direct Freeroam Sandbox**: Non-functional story mode has been streamlined; launches straight into sandbox freeroam.
- 🎨 **Resolution Quality Presets**: 1-click presets for **360p (Fastest)**, **480p**, **540p (Balanced)**, **720p (HD)**, or custom render scales.
- 🧠 **Anti-Crash Scudo Memory Guard**: Re-engineered Depth and Framebuffer allocations to stay strictly within Android's allocator ceilings.
- ⏱️ **Extended Session Stability (`SettingsOptimizer`)**: Active cache eviction and disabled background replay recording buffers (`-noreplay -nomirrors -disableRadio`), eliminating RAM leaks for uninterrupted gameplay.
- 🎮 **Peer-to-Peer Local Multiplayer**: Zero-latency UDP networking allowing multiple players to explore Los Santos together over Hotspot or Wi-Fi.

---

## 📱 Hardware Requirements

| Component | Minimum | Recommended |
| :--- | :--- | :--- |
| **OS** | Android 10.0 or higher | Android 12 / 13 / 14 |
| **SoC / Chipset** | MediaTek Helio G80 / Snapdragon 680 | MediaTek Helio G99 / Dimensity 8200 / Dimensity 8300 Ultra / Snapdragon 8 Gen 1+ |
| **GPU** | ARM Mali-G52 / Adreno 610 | ARM Mali-G57, G68, G77, G615 / Adreno 642L+ |
| **RAM** | 4 GB Physical RAM + Virtual zRAM | **6 GB – 8 GB+ Physical RAM** (Tested smooth on Poco X6 Pro 8GB) |
| **Storage** | 15 GB free internal storage | 25 GB free internal storage |

---

## 📥 Download & Official Community

> [!IMPORTANT]
> **Legal Notice**: This repository hosts **ONLY** the open-source launcher, compatibility layer, and optimization scripts. It does **NOT** host or distribute copyrighted Rockstar Games `.rpf` asset archives.
>
> To access the pre-compressed asset package (`game-import.zip`) and direct community mirrors, join our **Official Telegram Community**:

👉 **[Join Official Telegram Channel & Chat](https://t.me/+BJNsRLeI77g0ZTM1)**

---

## 🚀 Installation & First Launch

1. **Install the APK**:
   - Download **`GTA5_Mobile_v1.3_Release.apk`** from the [Releases](https://github.com/shoaibshakil/gta5-mobile-runtime/releases) tab or our Telegram channel.
   - Install the APK on your device.
2. **Download the Game Data**:
   - Download the complete `game-import.zip` from our [Telegram Channel](https://t.me/+BJNsRLeI77g0ZTM1).
   - Place `game-import.zip` into your phone's **Downloads** folder (`/sdcard/Download/`).
3. **Import Data**:
   - Open the **GTA 5** app.
   - Tap **"IMPORT GAME ZIP"** and select `game-import.zip`.
   - The app will extract the assets into private storage (takes 3–5 minutes).
4. **Choose Settings & Launch**:
   - Select your resolution preset (**360p** for low-end, **540p** for Dimensity/Snapdragon midrange, **720p** for flagships).
   - Select **Traffic Density** (choose **Light** or **Off** for maximum FPS).
   - Enable **AMD FSR 1.0** for adaptive edge sharpening.
   - Tap **START GTA V (OPTIMIZED RUNTIME)**.
   - On the first launch, Cranelift compiles `game.wasm` into a native ARM64 binary (`game.cwasm`). This takes 1–3 minutes. Future launches start instantly!

---

## 👥 How to Play Multiplayer with Friends

No internet connection or data usage required! Works seamlessly via direct phone-to-phone Hotspot or local Wi-Fi:

```
[HOST PHONE]                                         [JOINING FRIEND]
Personal Hotspot / Wi-Fi: Active                     Connected to same Hotspot / Wi-Fi
Host Session: [✔] CHECKED                            Host Session: [ ] UNCHECKED
Server IP: Auto-detected (e.g. 192.168.0.108)        Server IP: Type Host's IP (192.168.0.108)
     │                                                    │
     └────────────────── UDP Port 7777 / 6672 ────────────┘
```

1. **Connect Phones**:
   - Connect both devices to the same Wi-Fi router, or turn ON **Personal Hotspot** on one phone and connect the other phone to it.
2. **Host Phone Setup**:
   - Open GTA 5 Launcher.
   - Check **Multiplayer (Muguet UDP)**: `ON`
   - Check **Host a session**: `ON`
   - Note your cyan IP address displayed on the screen (e.g. `192.168.0.108`).
   - Enter your Player Name and tap **Play**.
3. **Joining Phone Setup**:
   - Open GTA 5 Launcher.
   - Check **Multiplayer (Muguet UDP)**: `ON`
   - Leave **Host a session**: `OFF` (UNCHECKED)
   - In **Enter Host Phone's IP Address (When Joining)**, enter the Host's IP (e.g. `192.168.0.108`).
   - Enter your Player Name and tap **Play**.
4. Both players will sync into the same Los Santos session with synchronized player positions, vehicles, and world physics!

---

## 🎨 Graphics Quality & Resolution Presets

In the app launcher screen, choose pre-configured resolution profiles:

| Quality Preset | Render Scale Value | Internal Resolution | Target FPS | Best For |
| :--- | :---: | :---: | :---: | :--- |
| **360p (Fastest)** | **`0.35`** | `560 × 252` | 20 – 30 FPS | Budget Phones (Helio G80/G85, Snapdragon 680) |
| **480p (Performance)** | **`0.40`** | `800 × 360` | 25 – 30 FPS | Cool Phone & Zero Lag cruising |
| **540p (Balanced)** | **`0.45` – `0.50`** | `1040 × 468` | 20 – 30+ FPS | **Poco X6 Pro (Dimensity 8300 Ultra) Recommended** |
| **720p (HD Native)** | **`0.55` – `0.65`** | `1360 × 612` | 20 – 25 FPS | Crisp, sharp visuals on Dimensity 9000+ / Snapdragon 8 Gen series |
| **1080p (Ultra Sharp)** | **`0.75` – `1.00`** | `1600 × 720` | 15 – 25 FPS | Flagship SoCs |

---

## 🛠️ Universal MediaTek One-Click Optimizer

If you are experiencing stuttering on a MediaTek device, connect your phone to a PC via USB (with USB Debugging enabled) and run:

```bash
python mediatek_universal_optimizer.py
```

This tool automatically queries `/proc/meminfo` and `getprop`, detects your SoC tier, and configures the optimal RAM heap budget, LOD bias, and Mali rendering flags.

---

## 🔮 Future Roadmap

- [ ] **Dual-Mode Touch Controller**: Interactive on-screen toggle button to switch seamlessly between **Walking Controls** (360° joystick, aim, punch) and **Driving Controls** (left/right steer buttons, gas, brake, handbrake).
- [ ] **Audio ALSA Low-Latency Buffer Engine**: Dedicated ring buffer management to eliminate ALSA underruns on budget SoCs.
- [ ] **Dynamic Resolution Scaling (DRS)**: Real-time resolution adjustment during intense high-speed police chases.
- [ ] **Dedicated Online 4G/5G Relay Servers**: Play over mobile data across different cities without local hotspots.
- [ ] **Street & Stunt Racing Gamemodes**: Glowing 3D checkpoints, countdown start grids, and race lap timers.
- [ ] **Vehicle & Weapon Spawner Menu**: Quick in-game touch menu to spawn sports cars, bikes, helicopters, and weapons.

---

## ⚖️ Legal Disclaimer

This project is an experimental, non-commercial research compatibility layer and launcher created for educational purposes. 

- This repository does **NOT** contain, redistribute, or reverse-engineer proprietary binary code or copyrighted asset files (audio, models, textures, or `.rpf` archives) owned by **Rockstar Games** or **Take-Two Interactive**.
- All game trademarks, logos, and character names are the registered intellectual property of Rockstar Games and Take-Two Interactive.
- Users must extract and utilize their own legitimate game archives.
