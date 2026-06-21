<div align="center">

<img src="https://pr.opop.eu.org/Frame_2.png" width="100" alt="VoxelPort" />

# VoxelPort

**Host your Minecraft server over the internet, no port forwarding.**  
No VPN. No router config. Players join with vanilla Minecraft.

[![Discord](https://img.shields.io/badge/Discord-Join-5865f2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/Fbqx76j5US)
[![License: MIT](https://img.shields.io/badge/License-MIT-00FFB2?style=flat-square)](https://github.com/VOXELPORT)
[![Website](https://img.shields.io/badge/Website-voxelport.in-00FFB2?style=flat-square)](https://www.voxelport.in)

</div>

---

## Overview

VoxelPort is a Minecraft networking project that lets server owners publish a server through the VoxelPort relay network. Your server connects out to the relay, the relay assigns a public address, and players join normally from Minecraft Multiplayer.

```text
Install plugin or mod       ->  paste your free Discord token
Run /voxelport status       ->  play.voxelport.in:25312
Friends paste the address   ->  connected with vanilla Minecraft
```

Players do not need to install anything.

---

## Repositories

| Repo | What it is |
|---|---|
| [Paper Plugin](#paper-plugin) | Paper server plugin for Paper 1.21+ servers |
| [Fabric Mod](#fabric-mod) | Fabric server mod for Minecraft 26.x / Java 25 servers |
| [Server Infrastructure](#server-infrastructure) | Relay proxy and Discord bot behind the network |
| [Website](#website) | Marketing, docs, and status site at [www.voxelport.in](https://www.voxelport.in) |

---

## Paper Plugin

A **Paper server plugin** that connects your self-hosted Minecraft server to the relay, giving it a public address like `play.voxelport.in:25312`. Players connect with unmodified Minecraft.

**Stack:** Java 21, Paper 1.21+

**Key features:**

- Public address without port forwarding
- Vanilla clients connect directly
- Free token issued through Discord with `/gettoken`
- Encrypted `wss://voxelport.in` connection to the relay
- `/voxelport status` shows public address and relay health
- Drop-in JAR, no separate tunnel app

**Quick start:**

```bash
cd plugin
./gradlew build
```

Output:

```text
plugin/build/libs/voxelport-plugin-1.0.0.jar
```

Install the JAR in `plugins/`, add your token to `plugins/VoxelPort/config.yml`, then start the server.

---

## Fabric Mod

A **Fabric server mod** that brings the same relay flow to Fabric servers. It uses the same token and public-port relay protocol as the Paper plugin.

**Stack:** Java 25, Fabric Loader 0.18.6+, Minecraft 26.x

**Key features:**

- Dedicated server support through `/voxelport` commands
- Same public address flow: `play.voxelport.in:<assigned-port>`
- Token saved locally in `config/voxelport/settings.properties`
- WebSocket frame buffering and serialized sends to avoid packet-stream corruption
- Client-side legacy singleplayer room-code UI is still present, but server mode is the recommended path

**Server commands:**

```mcfunction
/voxelport token <token-from-discord-gettoken>
/voxelport start
/voxelport start <port>
/voxelport status
/voxelport address
/voxelport stop
```

**Quick start:**

```bash
cd VoxelPortMod
./gradlew build
```

Output:

```text
VoxelPortMod/build/libs/voxelport-mod-1.2.0.jar
```

Install the JAR in the Fabric server `mods/` folder, restart the server, save your token with `/voxelport token <token>`, then run `/voxelport start`.

---

## Server Infrastructure

The relay and Discord bot power the public network.

### relay

The Go WebSocket relay validates tokens, assigns public TCP ports, and bridges raw Minecraft traffic between vanilla clients and a registered server.

```bash
cd relay
go build ./...
```

### bot

The Discord bot issues server tokens and supports the community workflow around `/gettoken`, `/revoketoken`, and relay status.

```bash
cd bot
npm install
npm run build
```

---

## Website

The VoxelPort marketing, docs, and status site is deployed at [www.voxelport.in](https://www.voxelport.in).

**Stack:** React, Vite, Three.js, Lenis

```bash
cd website
npm install
npm run dev
npm run build
```

---

## How It Works

```text
PAPER / FABRIC SERVER        RELAY                 VANILLA CLIENT
---------------------        -----                 --------------
Register token      --wss->  voxelport.in
Assigned port       <------  play.voxelport.in:25312
                                           <--tcp--  Player joins address
Game traffic        <----->  proxy bridge  <----->  Minecraft client
```

1. The plugin or mod opens an outbound WebSocket to the relay.
2. It registers using a Discord-issued server token.
3. The relay validates the token and assigns a stable public TCP port.
4. Players join the public address from vanilla Minecraft.
5. Minecraft packets are bridged through the relay without being stored.

The relay is a bridge, not a game server. Your actual Minecraft server still runs on your machine or host.

---

## Discord Verification

Access to the relay is gated by membership in the [VoxelPort Discord server](https://discord.gg/Fbqx76j5US). Run `/gettoken` in Discord to receive a server token.

This helps prevent anonymous abuse without making players create a separate VoxelPort account.

---

## Relay Infrastructure

The relay currently runs on a node in India at `voxelport.in`.

| Region | Expected latency overhead |
|---|---|
| South Asia, Southeast Asia | < 80 ms |
| Middle East, East Asia | 80-150 ms |
| Europe | 150-250 ms |
| North America | 250-400 ms |
| South America, Australia | > 400 ms |

Additional nodes are planned as the network grows. [Check live status](https://www.voxelport.in/#/status).

---

## Contributing

VoxelPort welcomes contributors. See the [Join Us page](https://www.voxelport.in/#/join) for open roles.

1. Fork the relevant repository.
2. Make your changes.
3. Open a pull request against `main`.

Bug reports and feature requests go in the Issues tab of the relevant repository.

---

## Links

- [Website](https://www.voxelport.in)
- [Discord](https://discord.gg/Fbqx76j5US)
- [Paper Plugin on Hangar](https://hangar.papermc.io/voxelportt/VoxelPort)
- [Paper Plugin on Modrinth](https://modrinth.com/plugin/voxelportplugin)
- [VoxelPort GitHub](https://github.com/VOXELPORT)

---

## License

MIT. See individual repository license files.

VoxelPort is not affiliated with Mojang, Microsoft, Fabric, PaperMC, or Discord.  
Minecraft is a trademark of Mojang AB.

---

<div align="center">

Built by [trazhub](https://github.com/trazhub)

</div>
