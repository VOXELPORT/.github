<div align="center">

<img src="https://pr.opop.eu.org/Frame_2.png" width="100" alt="VoxelPort" />

# VoxelPort

**Host a Minecraft server over the internet — no port forwarding.**  
A Fabric mod and a desktop app, backed by relay infrastructure. No signup, no Discord, no token to copy.

[![License: MIT](https://img.shields.io/badge/License-MIT-00FFB2?style=flat-square)](https://github.com/VOXELPORT)
[![Website](https://img.shields.io/badge/Website-voxelport.in-00FFB2?style=flat-square)](https://www.voxelport.in)
[![Status](https://img.shields.io/badge/Status-Page-00FFB2?style=flat-square)](https://www.voxelport.in/#/status)

</div>

---

## Overview

VoxelPort connects a Minecraft server to VoxelPort-operated relay infrastructure. Your game or app opens an outbound encrypted WebSocket connection, the relay assigns a public TCP port, and players join that address from vanilla Minecraft — no mod or app install needed on their end.

```text
Install the mod or app      ->  device token is generated automatically
Start hosting                ->  play.voxelport.in:<assigned-port>
Friends paste the address    ->  connected with vanilla Minecraft
```

Players do not need to install anything.

---

## Repositories

| Repo | What it is |
|---|---|
| [VoxelPort](https://github.com/VOXELPORT/VoxelPort) | Fabric mod — host straight from your game or a dedicated server |
| [VoxelPort-App](https://github.com/VOXELPORT/VoxelPort-App) | Desktop app (Windows/Linux) — tunnels any local server, or installs and runs one for you (Vanilla/Paper/Fabric) |

---

## Fabric Mod

A **Fabric mod** that works for both singleplayer ("Open to LAN" + "Open to VoxelPort" from the pause menu) and dedicated servers.

**Stack:** Java 25, Fabric Loader 0.18.6+, Minecraft 26.x

**Key features:**

- Singleplayer: one click from the pause menu, no commands needed
- Dedicated server support through `/voxelport` commands
- Device token generated automatically on first launch — nothing to request or paste
- WebSocket frame buffering and serialized sends to avoid packet-stream corruption

**Server commands** (`/voxelport`, aliased `/voxel` and `/vp`):

```mcfunction
/voxelport start
/voxelport start <port>
/voxelport status
/voxelport address
/voxelport stop
```

`/voxelport token <token>` also exists as an advanced manual override — not needed normally.

**Quick start:**

```bash
cd VoxelPortMod
./gradlew build
```

Output: `VoxelPortMod/build/libs/VoxelPort-<version>.jar`

Install the JAR in the Fabric server's `mods/` folder, restart the server, then run `/voxelport start`.

---

## Desktop App

An Electron app (Windows/Linux) for people who don't want to touch a mod loader. It can tunnel any server you already run locally, or install and run a Vanilla, Paper, or Fabric server itself — with a RAM slider recommended from your PC's specs, Java detection, and a folder picker so server files can live on any drive.

---

## How It Works

<p align="center">
  <img src="https://raw.githubusercontent.com/VOXELPORT/VoxelPort/main/docs/how-it-works.svg" alt="How VoxelPort connects a host to players through the relay" width="900" />
</p>

1. The mod or app opens an outbound WebSocket to the relay.
2. It registers using its auto-generated device token.
3. The relay assigns a public TCP port.
4. Players join `play.voxelport.in:<assigned-port>` from vanilla Minecraft.
5. Minecraft traffic is bridged through the relay to your server — not stored.

The relay is a bridge, not a game server. Your world, mods, and player data stay on your own machine.

Check live status on the [VoxelPort status page](https://www.voxelport.in/#/status).

---

## Contributing

VoxelPort welcomes contributors — fork the relevant repository, make your changes, and open a pull request against `main`. Bug reports and feature requests go in that repository's Issues tab.

---

## Links

- [Website](https://www.voxelport.in)
- [Status Page](https://www.voxelport.in/#/status)
- [Fabric Mod](https://github.com/VOXELPORT/VoxelPort)
- [Desktop App](https://github.com/VOXELPORT/VoxelPort-App)

---

## License

MIT. See individual repository license files.

VoxelPort is not affiliated with Mojang, Microsoft, Fabric, or PaperMC.  
Minecraft is a trademark of Mojang AB.

---

<div align="center">

Built by [trazhub](https://github.com/trazhub)

</div>
