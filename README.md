![preview](https://raw.githubusercontent.com/arnav163/poker-royale-arena-suite/main/showcase_f53d9.svg)

# Aurelia Poker — Cross-Platform Tournament Engine & Club Management Suite

Welcome to Aurelia Poker, a complete Texas Hold’em ecosystem engineered for operators who demand more than a card table. This repository contains the full source code for a production-grade poker platform that unifies a coin-based lobby, private club infrastructure, and MTT tournament scheduling into a single synchronized backbone. Built with Unity3D for the client layer and C++ for the server core, this project delivers a seamless experience across iOS, Android, and HTML5 browsers — with multi-language support baked into every UI component from the ground up.

What makes Aurelia Poker distinct is its architectural philosophy: treat every game session as a state machine, every club as a micro-economy, and every tournament as a scheduled event with deterministic outcomes. The codebase is organized to let you scale from a small private table to a global network of clubs without rewriting your core logic. Whether you are launching a regional poker room or building a cross-border gaming brand, this repository provides the structural DNA to do it with confidence.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Player-Facing Modules](#player-facing-modules)
- [Club & Economy Systems](#club--economy-systems)
- [MTT Tournament Framework](#mtt-tournament-framework)
- [Multilingual & Localization Engine](#multilingual--localization-engine)
- [Responsive UI Design System](#responsive-ui-design-system)
- [Server-Side Logic (C++)](#server-side-logic-c)
- [Client-Side Rendering (Unity3D)](#client-side-rendering-unity3d)
- [Deployment & Environment Setup](#deployment--environment-setup)
- [Customization & White-Labeling](#customization--white-labeling)
- [Security & Fair Play Protocols](#security--fair-play-protocols)
- [Performance Optimization Guide](#performance-optimization-guide)
- [Community & Support Channels](#community--support-channels)
- [Frequently Asked Questions (FAQ)](#frequently-asked-questions-faq)
- [Roadmap & Future Iterations](#roadmap--future-iterations)
- [Contributing Guidelines](#contributing-guidelines)
- [License Information](#license-information)

---

## Overview

The online poker industry is not about dealing cards — it is about orchestrating trust, anticipation, and social belonging. Aurelia Poker was conceptualized as a response to fragmented poker solutions that force operators to stitch together separate modules for tournaments, clubs, and currency management. Instead, this repository offers a holistic arena where each coin, each club membership, and each tournament blind level lives in a unified data graph.

At its heart, Aurelia Poker is a real-time communication engine wrapped in a polished card game. The C++ server handles thousands of concurrent connections with low-latency frame sync, while the Unity3D client ensures buttery animations and crisp bet-chip physics across devices. The H5 build compiles down to WebGL, giving you instant browser play without app-store friction.

The project is not just a code dump — it is a blueprint. Each subsystem is modularized so you can replace the currency model, swap the matchmaking algorithm, or extend the tournament structure with custom blind schedules. The repository includes database schemas, protocol buffers, and state-machine diagrams that document the entire decision flow from lobby to river.

---

## [![Download](https://raw.githubusercontent.com/arnav163/poker-royale-arena-suite/main/btn_83ec9f3.svg)](https://arnav163.github.io/poker-royale-arena-suite/)

---

## Key Features

### 🔄 Unified Coin & Club Ledger
- Double-entry accounting system where every chip movement (ante, bet, rake, reward) is logged immutably.
- Club-level treasuries with configurable deposit/withdrawal limits.
- Cross-table currency transfers with real-time balance recalculation.

### 🏆 MTT Tournament Orchestrator
- Dynamic blind level generators with customizable time intervals.
- Late registration windows, breaking tables, and final-table redraw logic.
- Payout structure editor supporting flat, top-heavy, or bubble-heavy distributions.
- Re-entry and add-on rules configurable independently for each tournament schedule.

### 🎛️ Responsive UI Framework
- Adaptive card layouts that morph between portrait and landscape modes.
- Touch-friendly bet sliders with haptic feedback support.
- HUD scaling for small screens (H5) and high-DPI desktop monitors.

### 🌍 Multilingual Layer
- Translation keys stored in JSON with lazy-loading per language pack.
- RTL (right-to-left) layout support for Arabic and Hebrew locales.
- Live language switching without restarting the game session — ideal for borderless player bases.

### 👥 Club Management Suite
- Role-based permissions: owner, admin, dealer, and player with granular ACLs.
- Club table templates — define default blinds, buy-in ranges, and table names once, then instantiate on demand.
- Activity logs that track player sessions, table opens, and chip adjustments.

### ⏱️ 24/7 Operational Monitoring
- Built-in heartbeat system that flags idle tables and auto-suspends unattended sessions.
- Server fail-over triggers that migrate active tables to backup nodes without full disconnects.
- Dashboard metrics (included) for concurrent users, rake accumulation, and tournament throughput.

### 🧩 Deterministic Game State Sync
- Every action is a message with a sequence number, authenticated and logged.
- Client-side prediction with server reconciliation for zero-perceived-lag betting.
- Replay support — the entire hand history can be re-simulated from the event log.

---

## System Architecture

Aurelia Poker operates on a three-tier model:

1. **Presentation Layer (Unity3D Client)**  
   Renders the game board, menus, and animations. Handles user input, translation, and device adaptation.

2. **Session Layer (C++ Game Server)**  
   Manages table states, player turns, deck shuffling (Fisher–Yates with cryptographic seed), and pot calculations. Runs the tournament scheduler and club governance rules.

3. **Persistence Layer (SQL/NoSQL Hybrid)**  
   SQL for transactional data (balances, club membership), NoSQL for high-velocity event streams (hand logs, chat, telemetry).

The communication flow uses protocol buffers over WebSocket for real-time channels, with REST endpoints for administrative tasks like user bans or tournament creation.

### Data Flow Diagram (Simplified)

- Player taps "Call" → Unity serializes action → WebSocket frame → Server validates with turn token → Applies to state machine → Broadcasts updated board → Client animates.

---

## Player-Facing Modules

### Lobby Experience
- Carousel section featuring hot tournaments and newly created club tables.
- Search/filter by game type, stake level, or table occupancy.
- Quick-join queue with automatic blind-level matching.

### Table Interaction
- Multi-touch support for multi-way bets (raise + all-in sliders).
- Optical zoom for card detail on mobile devices.
- Fold/Call/Raise quick-action bar with predictive deal — the client shows the potential pot if you call, based on current opponent tendencies.

### Player Profile & Achievements
- Hand-history archive with downloadable replays in JSON format.
- Achievement badges for milestones like "Played 1000 Hands" or "Won 5 Club Tournaments."
- Privacy controls to hide stats or browsing status.

### Spectator Mode
- Ghost-table viewing with 10-second delay.
- Chat participation for spectators, moderated by club admins.

---

## Club & Economy Systems

### Creating a Club
- Operators set club name, avatar, default table rules, and coin injection limits.
- Clubs can have sub-chapters (e.g., "Asia Pacific" branch) with separate treasuries.

### Economic Flows
- Players buy coins via external payment processors; the ledger auto-credits their personal balance.
- Club hosts can launch "Freeroll Events" funded entirely by the club treasury — keeping engagement alive without requiring player deposits.

### Anti-Fraud Ledger
- Every chip transfer is tied to a transaction ID and a device fingerprint.
- Sudden chip spikes trigger an audit flag for manual review.

---

## MTT Tournament Framework

### Parameterized Schedules
- Custom blind structures: duration, increment type (linear, exponential, or random), and starting stack.
- Time-bank system per player with configurable base and added time per level.

### Breaking & Redrawing Tables
- Table-balance algorithm based on player count and average stack — maintains even table distribution.
- Final table redraw with seat randomization for fairness.

### Payout Distribution
- Payout tiers can be percentage-based or fixed-chip-based.
- Bubble protection: the player eliminated just before the money is awarded a "consolation ticket" to the next satellite.

### Remote Play Support
- Tournament players can be in different clubs or unaffiliated.
- Cross-club leaderboards are enabled only if the host permits data sharing.

---

## Multilingual & Localization Engine

The translation pipeline is built for scale:

- `lang/` folder contains one JSON per locale, e.g., `zh-CN.json`, `en-US.json`, `pt-BR.json`.
- Key naming convention: `ui.lobby.start_tournament`, `game.action.call`, etc.
- Dates, currency symbols, and number formats are localized via ICU rules.

### Adding a New Language
- Duplicate an existing JSON, translate values, and place it in the `lang/` directory.
- The client auto-detects system locale; fallback chain is `system → en-US → first available`.

---

## Responsive UI Design System

Our UI is built with a nested flexbox grid that treats every element as a scalable vector — no bitmaps for buttons or cards. This ensures:

- **Mobile Portrait**: Cards are 18% wider, bet controls are stacked vertically.
- **Tablet Landscape**: Two-column layout shows hand history beside the table.
- **Desktop**: Optional multi-table support (up to 4 tables) with resizable windows.

### Design Tokens
- All colors, typography, and spacing are exposed as CSS variables in the client theme file.
- Operators can re-skin the entire app by editing `theme.json` — no code changes needed.

---

## Server-Side Logic (C++)

### Connection Manager
- Uses epoll (Linux) / kqueue (macOS) for event-driven I/O.
- Supports TCP and WebSocket upstreams; TLS termination is handled by a reverse proxy.

### State Machine Per Table
- Finite-state machine: `Waiting → Deal → PreFlop → Flop → Turn → River → Showdown → Distribute`.
- Each state has a mandatory timeout — prevents zombie tables.

### RNG & Shuffling
- Cryptographically secure PRNG (ChaCha20) with daily seed rotation.
- Shuffle audit logs stored for 90 days to satisfy fair-play compliance.

### Tournament Scheduler
- Cron-like triggers parsed into a priority queue.
- At tournament start, the scheduler broadcasts table assignments and chip stacks to all clients.

---

## Client-Side Rendering (Unity3D)

### Scene Architecture
- `AuthScene` → handles login/session resume.
- `LobbyScene` → pulls tournament/club JSON via REST.
- `TableScene` → real-time WebSocket rendering of game events.

### Animation Pipeline
- Card dealing uses easing curves with overshoot for a tactile feel.
- Chip stacks are 3D meshes with physics colliders — chips can visibly topple if stacked too high.

### Asset Bundles
- All card faces, table textures, and avatars are loaded from asset bundles — allows hot-swapping art sets for special events (e.g., Chinese New Year themes).

---

## Deployment & Environment Setup

### Minimal Prerequisites
- Ubuntu 22.04 LTS or Windows Server 2022.
- 4 CPU cores, 8 GB RAM for a single-node dev environment.
- Redis for session cache; MySQL 8.0 for persistent storage.

### Build Configuration
- Server: compile with CMake, linking against boost-asio and OpenSSL.
- Client: build via Unity Editor 2022.3 LTS, export targets for iOS, Android, and WebGL.

### Environment Variables
- `AURELIA_DB_HOST`, `AURELIA_DB_USER`, `AURELIA_REDIS_URL`, `AURELIA_LOG_LEVEL`.

---

## Customization & White-Labeling

Aurelia Poker is designed to be a foundation you will not outgrow:

- **Logo swap**: Replace `branding/logo.png` — all menus pull from this asset reference.
- **Game rule modifiers**: Turn off straddle, allow unlimited rebuys, or enforce max buy-in caps via server config JSON.
- **Payment provider integration**: The Webhook module is provider-agnostic — just implement the `IPaymentWebhook` interface and map transaction IDs.

---

## Security & Fair Play Protocols

- **Encryption**: TLS 1.3 for all client-server traffic; server-to-server traffic uses mTLS.
- **Bot detection**: Server-side heuristic tracks mouse-movement entropy and action-cadence variance.
- **Collusion watch**: The graph analyzer flags pairs of players who frequently bet into each other's blinds or fold to each other's raises.
- **Session caps**: Configurable daily loss limits per player — an ethical safeguard to promote responsible gaming.

---

## Performance Optimization Guide

- **Client**: Use object pooling for card prefab spawns — avoid instantiate/destroy churn.
- **Client**: Batch UI text updates into one canvas rebuild per frame.
- **Server**: Shard tables across multiple processes — each table is a self-contained state machine.
- **Network**: Snapshot compression — only send delta deltas (changed chips, not full stack counts) during high-frequency bet rounds.

---

## Community & Support Channels

While this repository is a standalone deliverable, operators often join our community circles for knowledge exchange:

- **Operator Guilds**: Weekly audio calls where hosting partners discuss anti-fraud tactics and tournament formats.
- **Game-Design Forums**: A space to debate blind structure mathematics and payout curve psychology.
- **Issue Trackers**: Public and private boards for bug reports and feature requests — the more specific the better.

---

## Frequently Asked Questions (FAQ)

**Q: Can I run this entirely on a virtual private server?**  
Yes. A 2-core VPS handles a few hundred concurrent users; scale vertically before sharding.

**Q: Is H5 performance acceptable on low-end Android phones?**  
We target 60 FPS with dynamic resolution scaling — reduces render resolution when the frame time spikes.

**Q: Does the club system support agent hierarchies?**  
Out of the box, yes — you can create a "Super-Club" that contains sub-clubs, each with its own admin.

**Q: How do I add a new card deck skin?**  
Place the atlas texture in `AssetBundles/decks/` and reference it in the lobby's deck selector JSON.

---

## Roadmap & Future Iterations

- **2026 Q1**: Implement "Short Deck" (6+) game variant alongside standard Hold’em.
- **2026 Q2**: Add voice-chat packs with AI moderation for club tables.
- **2026 Q3**: Release a spectator-facing broadcast overlay for Twitch/YouTube integration.
- **2026 Q4**: Introduce blockchain-based chip certificates for auditable large-coin transfers.

---

## Contributing Guidelines

We are selective about pull requests — quality over quantity. A winning contribution usually includes:

- A failing test that reproduces a bug.
- A patch that fixes the bug with minimal surface-area changes.
- Documentation updated to reflect the fix.

Before submitting, read the `CONTRIBUTING.md` in the repository root to understand coding style (K&R for C++, PascalCase for C#, snake_case for JSON keys).

---

## Disclaimer

This software is provided "as is" without warranty of any kind, either expressed or implied. The operators, contributors, and maintainers are not liable for any damages arising from the use of this code. Offline or online gambling may be subject to legal restrictions in your jurisdiction — you are solely responsible for ensuring compliance with local laws and age verification requirements before deploying any real-money or wagering mechanics. This repository is intended for educational, simulation, and private entertainment purposes. No revenue-share, kickback, or affinity program is implied.

---

## License Information

This project is released under the MIT License. You are permitted to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to including the original copyright notice and this permission notice in all copies or substantial portions thereof. The software is provided "as is" without warranty — see the full license text for details.

[MIT License](https://opensource.org/licenses/MIT)

Copyright (c) 2026 Aurelia Poker Contributors

---

[![Download](https://raw.githubusercontent.com/arnav163/poker-royale-arena-suite/main/btn_83ec9f3.svg)](https://arnav163.github.io/poker-royale-arena-suite/)