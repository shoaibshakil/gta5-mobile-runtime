# 🛑 Los Santos Mobile Runtime (GTA V Android WebPort — Final Edition)

> [!IMPORTANT]
> ### 📦 ARCHIVED & END-OF-LIFE NOTICE (FINAL MILESTONE v1.4)
> **This repository is officially ARCHIVED and in READ-ONLY mode. Development has concluded.**
>
> We have reached the maximum architectural ceiling possible on the 32-bit WebAssembly (WASM) mobile runtime. All planned optimization goals—including the **64 MB anti-crash memory buffer**, **local peer-to-peer multiplayer**, **AMD FSR 1.0 CAS sharpening**, and **always-on hardware-accelerated touch controls**—have been fully achieved and stabilized.
> 
> * **Final Releases:** Stable builds (`v1.3` and `v1.4`) remain permanently available in the [Releases](https://github.com/shoaibshakil/gta5-mobile-runtime/releases) section.
> * **Support & Issues:** Issues and Pull Requests are closed. No further updates or feature requests will be accepted.

---

An ultra-optimized, high-performance runtime for running Grand Theft Auto V assets on ARM64 Android devices using Cranelift JIT compilation, WebAssembly, and native Vulkan/WebGPU acceleration.

Specifically fine-tuned for MediaTek (Helio G & Dimensity) and Snapdragon devices to prevent out-of-memory allocation crashes and thermal throttling while preserving crisp visual fidelity.

---

## 📊 Real-Device Benchmark & FPS Testing

Tested performance figures from our development devices on the final builds:

| Device | Specs / Chipset | RAM | Tested FPS Range | Current Status |
| :--- | :--- | :--- | :--- | :--- |
| **Poco X6 Pro** | MediaTek Dimensity 8300 Ultra (Mali-G615) | 8 GB | **20 – 30+ FPS** | **Playable & Stable** (20+ FPS stable in freeroam and vehicle cruising) |
| **Vivo Y20G** | MediaTek Helio G80 (Mali-G52 MC2) | 6 GB | **5 – 12 FPS** | **Experimental** (CPU-bound 32-bit WASM software emulation) |

> [!NOTE]
> **Performance Notice:** On midrange to flagship chips (Dimensity 8300 Ultra / Snapdragon 8 Gen series with 8 GB+ RAM), the runtime delivers a stable 20–30+ FPS. Entry-level budget SoCs (Helio G80/G85) face severe CPU bottlenecking due to 32-bit WASM emulation overhead. 

---

## ⚡ What Was Achieved Across v1.3 & v1.4 (Final Milestone)

* 🎮 **Always-On Touch Controls & Hardware Acceleration (v1.4):** Fixed the bug where custom OS game overlays (such as Xiaomi Game Turbo or keymappers) caused on-screen buttons to disappear. Bypassed software layers for direct GPU blitting on MediaTek Mali & Snapdragon Adreno GPUs.
* 🌐 **Full Working Local Multiplayer (UDP):** Connect with friends seamlessly over the same Wi-Fi or mobile personal hotspot with zero data usage.
* 🔍 **Auto Wi-Fi IP Detection:** Launcher automatically queries and displays your device's active local IP address in cyan with step-by-step Host & Client instructions.
* ⚡ **AMD FSR 1.0 (Edge-Adaptive CAS Sharpening):** Built-in FidelityFX Contrast Adaptive Sharpening to reconstruct sharp 1080p images from 360p/540p render scales.
* 🚙 **Driving Memory Crash & Lag Fix (64 MB Buffer):** Re-tuned file streaming buffers to 64 MB (`maxFileStoreSize: 65536`) and removed conflicting negative LOD biases, completely stopping the 30 FPS -> 5-2 FPS drop and eliminating the 3.0 GB WASM memory ceiling crash during fast vehicle travel.
* 📱 **Scaleform DirectX 11 Pipeline:** Restored radar minimap and in-game cellphone overlay rendering with full alpha blending.
* 🌫️ **Natural Fog Distance Culling:** Dynamically limits render distances of high-memory distant props and building LODs past 90m to eliminate GPU lag in dense downtown areas.
* 🔊 **Restored Core Audio (SFX):** Vehicle engine revs, footsteps, gunshots, and collisions are unmuted, while missing radio stream threads remain silenced to prevent CPU audio spinlocks.

---

## 📦 What Makes This Runtime Special?

Standard GTA V requires over 100 GB of storage and 8+ GB of VRAM. This specialized mobile port features:

* 📦 **Ultra-Compressed Game Footprint:** Stripped of redundant filler and multi-language audio packs down to a lightweight portable package size (saving over 85 GB of storage).
* 🚦 **In-App Traffic & Pedestrian Switcher:**
  * **Off (Maximum FPS / Zero Lag):** Eliminates ambient cars and ped AI load completely.
  * **Light (Anti-Lag & Cool Phone):** Only 2–3 ambient cars for smooth cruising without heating.
  * **Balanced & High:** Moderate to full city density.
* 🎮 **Direct Freeroam Sandbox:** Launches straight into sandbox freeroam without non-functional story mission roadblocks.
* 🎨 **Resolution Quality Presets:** 1-click presets for 360p (Fastest), 480p, 540p (Balanced), 720p (HD), or custom render scales.
* 🧠 **Anti-Crash Scudo Memory Guard:** Re-engineered Depth and Framebuffer allocations to stay strictly within Android's allocator ceilings.
* ⏱️ **Extended Session Stability (SettingsOptimizer):** Active cache eviction and disabled background replay recording buffers (`-noreplay -nomirrors -disableRadio`), eliminating RAM leaks for uninterrupted gameplay.

---

## 📱 Hardware Requirements

| Component | Minimum | Recommended |
| :--- | :--- | :--- |
| **OS** | Android 10.0 or higher | Android 12 / 13 / 14 |
| **SoC / Chipset** | MediaTek Helio G80 / Snapdragon 680 | MediaTek Dimensity 8200 / 8300 Ultra / Snapdragon 8 Gen 1+ |
| **GPU** | ARM Mali-G52 / Adreno 610 | ARM Mali-G615 / Adreno 642L+ |
| **RAM** | 4 GB Physical RAM + Virtual zRAM | 6 GB – 8 GB+ Physical RAM |
| **Storage** | 15 GB free internal storage | 25 GB free internal storage |

---

## 📥 Downloads & Official Community

> [!IMPORTANT]
> **Legal Notice:** This repository hosts ONLY the open-source launcher, compatibility layer, and optimization scripts. It does NOT host or distribute copyrighted Rockstar Games `.rpf` asset archives.

To access the pre-compressed asset package (`game-import.zip`) and community mirrors, join our Official Telegram Community:
👉 [Join Official Telegram Channel & Chat](https://t.me/+BJNsRLeI77g0ZTM1)

---

## 🚀 Installation & First Launch

1. **Install the APK:**
   * Download the latest release APK from the [Releases](https://github.com/shoaibshakil/gta5-mobile-runtime/releases) tab or our Telegram channel.
   * Install the APK on your device.
2. **Download the Game Data:**
   * Download the complete `game-import.zip` (or multi-part split) from our [Telegram Channel](https://t.me/+BJNsRLeI77g0ZTM1).
   * Place the files into your phone's storage.
3. **Import Data:**
   * Open the GTA 5 app.
   * Tap **IMPORT GAME ZIP** and select the data package.
   * The app will extract the assets into private storage (takes 3–5 minutes).
4. **Choose Settings & Launch:**
   * Select your resolution preset (360p for low-end, 540p for Dimensity/Snapdragon midrange, 720p for flagships).
   * Select Traffic Density (**Light** or **Off** recommended for highest FPS).
   * Enable **AMD FSR 1.0** for adaptive edge sharpening.
   * Tap **START GTA V (OPTIMIZED RUNTIME)**.

*Note: On the first launch, Cranelift compiles `game.wasm` into a native ARM64 binary (`game.cwasm`). This takes 1–3 minutes. Future launches start instantly!*

---

## 👥 How to Play Multiplayer with Friends

No internet connection or data usage required! Works seamlessly via direct phone-to-phone Hotspot or local Wi-Fi:

```text
[HOST PHONE]                                  [JOINING FRIEND]
Personal Hotspot / Wi-Fi: Active              Connected to same Hotspot / Wi-Fi
Host Session: [✔] CHECKED                     Host Session: [ ] UNCHECKED
Server IP: Auto-detected (e.g. 192.168.0.108) Server IP: Type Host's IP (192.168.0.108)
      │                                             │
      └────────────────── UDP Port 7777 / 6672 ─────┘
```

1. **Connect Phones:** Connect both devices to the same Wi-Fi router, or turn ON Personal Hotspot on one phone and connect the second phone to it.
2. **Host Phone:**
   * Open GTA 5 Launcher.
   * Enable **Multiplayer (Muguet UDP)**.
   * Check **Host a session**.
   * Note your cyan IP address displayed on the screen (e.g., `192.168.0.108`).
   * Enter your Player Name and tap **Play**.
3. **Joining Phone:**
   * Open GTA 5 Launcher.
   * Enable **Multiplayer (Muguet UDP)**.
   * Leave **Host a session** unchecked.
   * In the IP box, type the Host's IP address.
   * Enter your Player Name and tap **Play**.

---

## 🏁 Project Conclusion & Archival Reason

This project has officially reached the end of its development roadmap. 

* **The 32-bit WASM Ceiling:** The closed-source WebAssembly runtime operates in a 32-bit address space (hard ceiling ~3 GB RAM). Advanced modifications like native vehicle script-hook injection, full HD commercial radio station packs, and uncompressed physics exceed this ceiling and cause memory allocator crashes.
* **Stable State:** All achievable goals (memory crash prevention, resolution downscaling, UDP multiplayer, and touch controls) have been completed.
* **The Future:** Further performance leaps for mobile GTA V will come from native ARM64 translation layers (such as Box64/Winlator and native Xbox 360 emulation).

---

## ⚖️ Legal Disclaimer

This project is an experimental, non-commercial research compatibility layer and launcher created strictly for educational purposes.
* This repository does **NOT** contain, redistribute, or reverse-engineer proprietary binary code or copyrighted asset files (audio, models, textures, or `.rpf` archives) owned by Rockstar Games or Take-Two Interactive.
* All game trademarks, logos, and character names are the registered intellectual property of Rockstar Games and Take-Two Interactive.
* Users must extract and utilize their own legitimate game archives.
