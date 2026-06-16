<div align="center">

<img src="https://pr.opop.eu.org/Frame_2.png" width="100" alt="VoxelPort" />

# VoxelPort

**Host Minecraft worlds over the internet with a 6-character room code.**  
No port forwarding. No VPN. No router config. Just play.

[![Discord](https://img.shields.io/badge/Discord-Join-5865f2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/EuDMWUuGpp)
[![License: MIT](https://img.shields.io/badge/License-MIT-00FFB2?style=flat-square)](VoxelPort%20Mod/LICENSE)
[![Website](https://img.shields.io/badge/Website-voxelport.in-00FFB2?style=flat-square)](https://voxelport.in)

</div>

---

## Overview

VoxelPort is a Minecraft networking tool that lets players share worlds and servers over the internet without touching their router. Traffic is bridged through a relay network — no port forwarding, no VPN, no extra accounts.

```
Host presses "Open to VoxelPort"  →  code G0GI5Z copied to clipboard
Friend pastes G0GI5Z              →  connected in seconds
```

---

## Repositories

| Repo | What it is |
|---|---|
| [VoxelPort Mod](#voxelport-mod) | Fabric client mod — share a singleplayer world with a room code |
| [VoxelPort Server](#voxelport-server) | Relay proxy, Discord bot, and Paper plugin — the infrastructure behind the network |
| [Website](#website) | Marketing and status site at [voxelport.in](https://voxelport.in) |

---

## VoxelPort Mod

> `F:\VoxelPort Mod`

A **Fabric client mod** that lets you share your Minecraft singleplayer world with friends via a short room code. Neither side needs to configure their router — traffic flows through the VoxelPort relay.

**Stack:** Java 25 · Fabric Loader 0.18.6+ · Minecraft 26.x

**Key features:**
- 6-character room codes (e.g. `G0GI5Z`) — no IP addresses shared
- Discord DM verification gates relay access (no new accounts)
- Live relay ping in the tab list header
- In-game relay URL settings screen
- Auth cached locally for 12 hours per device
- Zero runtime dependencies — no extra apps

**Quick start:**

```bash
./gradlew build
# Output: build/libs/voxelport-mod-X.X.X.jar
```

Place the JAR in your Minecraft `mods/` folder and join the [VoxelPort Discord](https://discord.gg/EuDMWUuGpp) for verification.

[Full documentation](VoxelPort%20Mod/README.md)

---

## VoxelPort Server

> `F:\VoxelPort Server`

The server-side infrastructure. Three components that work together to run the relay network and gate access via Discord.

### relay-proxy

The WebSocket relay that bridges connections between hosts and joiners (or between the Paper plugin and vanilla clients).

**Stack:** Go

```bash
cd "VoxelPort Server/relay-proxy"
go build -o relay .
./relay serve
```

### discord-bot

Handles Discord DM verification for the Fabric mod and token issuance for the Paper plugin. Users run `/gettoken` to register their server.

**Stack:** Node.js · `discord.js` 14

```bash
cd "VoxelPort Server/discord-bot"
npm install
npm start
```

### paper-plugin

A Paper plugin that connects a server to the relay, giving it a public address like `play.voxelport.in:25312`. Vanilla clients connect directly — no mod required on their end.

**Stack:** Java 21 · Paper 1.21+

```bash
cd "VoxelPort Server/paper-plugin"
./gradlew build
# Output: build/libs/voxelport-plugin-1.0.0.jar
```

Drop the JAR into your server's `plugins/` folder, add your token to `plugins/VoxelPort/config.yml`, and start the server.

[Paper plugin documentation](VoxelPort%20Server/paper-plugin/README.md)

---

## Website

> `F:\Website`

The VoxelPort marketing and status site, deployed at [voxelport.in](https://voxelport.in).

**Stack:** React 19 · Vite · Tailwind CSS 4 · Three.js (`@react-three/fiber`) · Lenis (smooth scroll)

```bash
cd Website
npm install
npm run dev      # local dev server
npm run build    # production build → dist/
```

Deployed via Vercel (`vercel.json` in root).

---

## How It Works

```
HOST / PAPER SERVER             RELAY                        JOINER / VANILLA CLIENT
───────────────────             ─────                        ───────────────────────────
Open to VoxelPort   ──ws──▶  voxelport.in  ◀──ws──  Paste room code
Get code: G0GI5Z    ◀──────  assigns room            ──────▶  Connect to room
Game traffic        ──────▶  proxy bridge             ──────▶  Receives packets
```

1. Host or Paper plugin opens a WebSocket to the relay and registers
2. Relay assigns a room code or TCP port and holds the connection
3. Joiner or vanilla client connects — relay bridges the two sockets
4. Minecraft packets flow through the bridge without being read or stored
5. Relay tears down the session when either side disconnects

The relay is a stateless bridge. It does not inspect or persist game traffic.

---

## Discord Verification

Access to the relay is gated by Discord membership in the [VoxelPort server](https://discord.gg/EuDMWUuGpp).

- **Fabric mod users** — enter your Discord username in-game; the bot DMs you a 6-digit code
- **Paper plugin users** — run `/gettoken` in Discord to receive a server token

This prevents anonymous abuse of the relay without requiring a separate account.

---

## Relay Infrastructure

The relay currently runs on a single node in **India** (`voxelport.in`).

| Region | Expected latency overhead |
|---|---|
| South Asia, Southeast Asia | < 80 ms |
| Middle East, East Asia | 80–150 ms |
| Europe | 150–250 ms |
| North America | 250–400 ms |
| South America, Australia | > 400 ms |

Additional nodes in Europe and North America are planned as the project scales. [Check live status](https://voxelport.in/#/status)

---

## Contributing

VoxelPort welcomes contributors across all repos. See the [Join Us page](https://voxelport.in/#/join) for open roles.

1. Fork the relevant repo
2. Make your changes
3. Open a pull request against `main`

Bug reports and feature requests go in the Issues tab of the relevant repository.

---

## Links

- [Website](https://voxelport.in)
- [Discord](https://discord.gg/EuDMWUuGpp)
- [Fabric Mod on Modrinth](https://modrinth.com/mod/voxelport)
- [Paper Plugin on Hangar](https://hangar.papermc.io/trazhub/VoxelPort)
- [Paper Plugin on Modrinth](https://modrinth.com/plugin/voxelport)

---

## License

MIT — see individual repository LICENSE files.

VoxelPort is not affiliated with Mojang, Microsoft, Fabric, or Discord.  
"Minecraft" is a trademark of Mojang AB.

---

<div align="center">

Built by [trazhub](https://github.com/trazhub)

</div>
