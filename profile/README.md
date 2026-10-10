<div align="center">

<img src="https://voxelport.in/logo.png" width="100" alt="VoxelPort" />

# VoxelPort

**Host a Minecraft server over the internet — no port forwarding.**  
One desktop app, backed by relay infrastructure. No signup, no Discord, no token to copy.

[![License: MIT](https://img.shields.io/badge/License-MIT-5FAE3B?style=flat-square)](https://github.com/VOXELPORT)
[![Website](https://img.shields.io/badge/Website-voxelport.in-5FAE3B?style=flat-square)](https://voxelport.in)
[![Status](https://img.shields.io/badge/Status-Page-5FAE3B?style=flat-square)](https://voxelport.in/#/status)
[![Download](https://img.shields.io/github/v/release/VOXELPORT/VoxelPort-App?label=Download&color=C8262B&style=flat-square)](https://github.com/VOXELPORT/VoxelPort-App/releases/latest)

</div>

---

## Overview

VoxelPort connects a Minecraft: Java Edition server to VoxelPort-operated relay infrastructure. The desktop app opens an outbound encrypted WebSocket connection, the relay assigns a public TCP port, and players join that address from vanilla Minecraft — nothing to install on their end.

```text
Install the app              ->  device token is generated automatically
Create or import a server    ->  the right Java is installed for you
Press Start, then Public     ->  play.voxelport.in:<assigned-port>
Friends paste the address    ->  connected with vanilla Minecraft
```

---

## Repositories

| Repo | What it is |
|---|---|
| [VoxelPort-App](https://github.com/VOXELPORT/VoxelPort-App) | Desktop app (Windows/Linux) — creates, imports or tunnels any Minecraft Java server |
| [relay](https://github.com/VOXELPORT/relay) | The Go relay server that bridges players to hosts |
| [website](https://github.com/VOXELPORT/website) | voxelport.in |

> The Fabric mod ([VoxelPort](https://github.com/VOXELPORT/VoxelPort)) is discontinued. Use the desktop app instead — it works with any server, including Fabric and modpacks.

---

## Desktop App

An Electron app for Windows and Linux (macOS soon).

- **New server:** pick Vanilla, Paper or Fabric and a version — VoxelPort downloads it and starts it.
- **Your server:** import an existing server folder, or tunnel one that's already running on any port.
- **Java handled for you:** the correct Eclipse Temurin version is downloaded and checksum-verified automatically, including Java 25 for Minecraft 26.1+.
- **Live console**, player count and relay ping, a RAM slider sized to your PC, and server files on any drive.
- **Direct routing:** connects straight to the relay for low ping, falling back to Cloudflare if a network blocks it.

**[Get it from the Microsoft Store](https://apps.microsoft.com/detail/9NGRX9CFNBD6)** ·
[Linux](https://github.com/VOXELPORT/VoxelPort-App/releases/latest/download/VoxelPort-Linux.tar.gz)

---

## How It Works

1. The app opens an outbound WebSocket to the relay.
2. It registers using its auto-generated device token.
3. The relay assigns a public TCP port.
4. Players join `play.voxelport.in:<assigned-port>` from vanilla Minecraft.
5. Minecraft traffic is bridged through the relay to your server — not stored.

The relay is a bridge, not a game server. Your world, mods and player data stay on your own machine.

Check live status on the [VoxelPort status page](https://voxelport.in/#/status).

---

## Contributing

Fork the relevant repository, make your changes, and open a pull request against `main`. Bug reports and feature requests go in that repository's Issues tab.

---

## License

MIT. See individual repository license files.

VoxelPort is not affiliated with Mojang, Microsoft, Fabric, or PaperMC.  
Minecraft is a trademark of Mojang AB.

---

<div align="center">

Built by [trazhub](https://github.com/trazhub)

</div>
