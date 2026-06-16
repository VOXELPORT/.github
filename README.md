<div align="center">

<img src="https://pr.opop.eu.org/Frame_2.png" width="100" alt="VoxelPort" />

# VoxelPort

**Host your Minecraft server over the internet — no port forwarding.**  
No VPN. No router config. Players join with vanilla Minecraft.

[![Discord](https://img.shields.io/badge/Discord-Join-5865f2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/Fbqx76j5US)
[![License: MIT](https://img.shields.io/badge/License-MIT-00FFB2?style=flat-square)](https://github.com/VOXELPORT/VoxelPortPlugin/blob/main/LICENSE)
[![Website](https://img.shields.io/badge/Website-voxelport.in-00FFB2?style=flat-square)](https://www.voxelport.in)

</div>

---

## Overview

VoxelPort is a Minecraft networking tool that lets you host a server over the internet without touching your router. Your server connects out to a relay network, which bridges every player connection — no port forwarding, no VPN, no extra accounts on your players' side.

```text
Drop the plugin in plugins/   ->  paste your free token
Run /voxelport status         ->  play.voxelport.in:25312
Friends paste the address     ->  connected with vanilla Minecraft
```

---

## Repositories

| Repo | What it is |
|---|---|
| [Paper Plugin](#paper-plugin) | The Minecraft server plugin — connects your server to the relay and gives it a public address |
| [Server Infrastructure](#server-infrastructure) | Relay proxy and Discord bot — the infrastructure behind the network |
| [Website](#website) | Marketing and status site at [www.voxelport.in](https://www.voxelport.in) |

---

## Paper Plugin

A **Paper server plugin** that connects your self-hosted Minecraft server to the relay, giving it a public address like `play.voxelport.in:25312`. Players connect with unmodified Minecraft — no mod required on their end.

**Stack:** Java 21 · Paper 1.21+

**Key features:**

- Public address without port forwarding — your server never opens a port
- Vanilla clients connect directly — nothing to install for players
- Free token issued via Discord (`/gettoken`) — no new account
- Encrypted `wss://` link to the relay — your home IP is never shared
- `/voxelport status` shows your public address and connection health in-game
- Single drop-in JAR — no separate agent app running alongside

**Quick start:**

```bash
./gradlew build
# output: build/libs/voxelport-plugin-1.0.0.jar
```

Drop the JAR into your server's `plugins/` folder, add your token to `plugins/VoxelPort/config.yml`, and start the server. Get a token in the [VoxelPort Discord](https://discord.gg/Fbqx76j5US).

[Full documentation](https://github.com/VOXELPORT/VoxelPortPlugin#readme)

---

## Server Infrastructure

The server-side infrastructure. Two components that run the relay network and gate access via Discord.

### relay-proxy

The WebSocket relay that bridges connections between the Paper plugin and vanilla clients.

**Stack:** Go

```bash
go build -o relay .
./relay serve
```

### discord-bot

Issues server tokens for the Paper plugin and verifies Discord membership. Users run `/gettoken` to register their server.

**Stack:** TypeScript · discord.js 14

```bash
npm install
npm start
```

---

## Website

The VoxelPort marketing and status site, deployed at [www.voxelport.in](https://www.voxelport.in).

**Stack:** React 19 · Vite · Three.js (@react-three/fiber) · Lenis

```bash
npm install
npm run dev      # local dev server
npm run build    # production build -> dist/
```

---

## How It Works

```text
PAPER SERVER                  RELAY                 JOINER / VANILLA CLIENT
------------                  -----                 -----------------------
Connect + register   --ws-->  voxelport.in
Get port: 25312      <------  assigns public port
                                            <--tcp--  Connect to the address
Game traffic         ------>  proxy bridge   ------>  Receives packets
```

1. The Paper plugin opens a WebSocket to the relay and registers with its token
2. The relay assigns a public TCP port and holds the connection
3. A vanilla client connects to that address — the relay bridges the two sockets
4. Minecraft packets flow through the bridge without being read or stored
5. The relay tears down the session when either side disconnects

The relay is a stateless bridge. It does not inspect or persist game traffic.

---

## Discord Verification

Access to the relay is gated by Discord membership in the [VoxelPort server](https://discord.gg/Fbqx76j5US). Run `/gettoken` in Discord to receive a server token for your Paper plugin.

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

Additional nodes in Europe and North America are planned as the project scales. [Check live status](https://www.voxelport.in/#/status)

---

## Contributing

VoxelPort welcomes contributors. See the [Join Us page](https://www.voxelport.in/#/join) for open roles.

1. Fork the relevant repo
2. Make your changes
3. Open a pull request against `main`

Bug reports and feature requests go in the Issues tab of the relevant repository.

---

## Links

- [Website](https://www.voxelport.in)
- [Discord](https://discord.gg/Fbqx76j5US)
- [Paper Plugin on Hangar](https://hangar.papermc.io/trazhub/VoxelPort)
- [Paper Plugin on Modrinth](https://modrinth.com/plugin/voxelport)

---

## License

MIT — see individual repository LICENSE files.

VoxelPort is not affiliated with Mojang, Microsoft, or Discord.  
"Minecraft" is a trademark of Mojang AB.

---

<div align="center">

Built by [trazhub](https://github.com/trazhub)

</div>
