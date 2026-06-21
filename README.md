<div align="center">

<img src="https://pr.opop.eu.org/Frame_2.png" width="100" alt="VoxelPort" />

# VoxelPort

**Minecraft relay tooling for VoxelPort servers.**  
Plugin and mod support for private VoxelPort relay infrastructure.

[![Discord](https://img.shields.io/badge/Discord-Join-5865f2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/Fbqx76j5US)
[![License: MIT](https://img.shields.io/badge/License-MIT-00FFB2?style=flat-square)](https://github.com/VOXELPORT)
[![Website](https://img.shields.io/badge/Website-voxelport.in-00FFB2?style=flat-square)](https://www.voxelport.in)

</div>

---

## Overview

VoxelPort is a Minecraft networking project made of a Paper plugin, a Fabric mod, a relay service, and a Discord bot. Server owners connect their Minecraft server to a configured relay, and players join through the address assigned by that relay.

```text
Install plugin or mod       ->  paste your Discord-issued token
Run /voxelport status       ->  relay-host.example:25312
Friends paste the address   ->  connected with vanilla Minecraft
```

Players do not need to install anything.

---

## Repositories

| Repo | What it is |
|---|---|
| [Paper Plugin](#paper-plugin) | Paper server plugin for Paper 1.21+ servers |
| [Fabric Mod](#fabric-mod) | Fabric server mod for Minecraft 26.x / Java 25 servers |

---

## Paper Plugin

A **Paper server plugin** that connects your self-hosted Minecraft server to the configured relay, giving it a join address like `relay-host.example:25312`. Players connect with unmodified Minecraft.

**Stack:** Java 21, Paper 1.21+

**Key features:**

- Join address without port forwarding
- Vanilla clients connect directly
- Free token issued through Discord with `/gettoken`
- Encrypted `wss://` connection to the relay
- `/voxelport status` shows join address and relay health
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

A **Fabric server mod** that brings the same relay flow to Fabric servers. It uses the same token and assigned-port relay protocol as the Paper plugin.

**Stack:** Java 25, Fabric Loader 0.18.6+, Minecraft 26.x

**Key features:**

- Dedicated server support through `/voxelport` commands
- Same assigned-address flow: `<relay-host>:<assigned-port>`
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

## Infrastructure

The relay service and Discord bot are VoxelPort-operated infrastructure. They validate tokens, assign relay ports, and bridge Minecraft traffic for registered plugin/mod servers.

Implementation details are intentionally kept out of this public README.

## How It Works

<p align="center">
  <img src="assets/readme/how-it-works.gif" alt="Animated VoxelPort relay flow" width="900" />
</p>

1. The plugin or mod opens an outbound WebSocket to the relay.
2. It registers using a Discord-issued server token.
3. The relay validates the token and assigns a stable TCP port.
4. Players join the assigned address from vanilla Minecraft.
5. Minecraft packets are bridged through the relay without being stored.

The relay is a bridge, not a game server. Your actual Minecraft server still runs on your machine or host.

Check service information and updates on the [VoxelPort status page](https://www.voxelport.in/#/status).

---

## Discord Verification

Access to the relay is gated by membership in the [VoxelPort Discord server](https://discord.gg/Fbqx76j5US). Run `/gettoken` in Discord to receive a server token.

This helps prevent anonymous abuse without making players create a separate VoxelPort account.

## Contributing

VoxelPort welcomes contributors. See the [Join Us page](https://www.voxelport.in/#/join), join the Discord, or open an issue in the relevant GitHub repository.

1. Fork the relevant repository.
2. Make your changes.
3. Open a pull request against `main`.

Bug reports and feature requests go in the Issues tab of the relevant repository.

---

## Links

- [Discord](https://discord.gg/Fbqx76j5US)
- [Website](https://www.voxelport.in)
- [Status Page](https://www.voxelport.in/#/status)
- [Join Us](https://www.voxelport.in/#/join)
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
