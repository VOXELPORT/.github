<div align="center">

<img src="https://voxelport.in/logo.png" width="100" alt="VoxelPort" />

# VoxelPort

**Host a Minecraft server from your PC or Android phone — no port forwarding.**  
One free, open-source app for Windows, Linux and Android, backed by relays in India and Europe. Friends need no account, and hosts sign in with Discord once. Works behind Jio and Airtel (CGNAT), and Java and Bedrock players can join the same server.

[![License: MIT](https://img.shields.io/badge/License-MIT-5FAE3B?style=flat-square)](https://github.com/VOXELPORT)
[![Website](https://img.shields.io/badge/Website-voxelport.in-5FAE3B?style=flat-square)](https://voxelport.in)
[![Status](https://img.shields.io/badge/Status-Page-5FAE3B?style=flat-square)](https://voxelport.in/status)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?style=flat-square)](https://discord.gg/JAUfmey2fP)
[![Download](https://img.shields.io/github/v/release/VOXELPORT/VoxelPort-App?label=Download&color=C8262B&style=flat-square)](https://github.com/VOXELPORT/VoxelPort-App/releases/latest)

</div>

---

## Overview

VoxelPort connects a Minecraft: Java Edition server to VoxelPort-operated relay infrastructure. The app (desktop or Android) opens an outbound encrypted WebSocket connection, the relay assigns a public TCP port, and players join that address from vanilla Minecraft — nothing to install on their end.

```text
Install the app, sign in with Discord  ->  a device key is generated automatically
Create or import a server              ->  the right Java is installed for you
Press Start, then Public               ->  play.voxelport.in:<assigned-port>
Friends paste the address              ->  connected with vanilla Minecraft
```

---

## Repositories

| Repo | What it is |
|---|---|
| [VoxelPort-App](https://github.com/VOXELPORT/VoxelPort-App) | Desktop app (Windows/Linux) — creates, imports or tunnels any Minecraft Java server. Plugin and mod installer included |
| [voxelport-mobile](https://github.com/VOXELPORT/voxelport-mobile) | Android app, hosts a Paper server on your phone |
| [relay](https://github.com/VOXELPORT/relay) | The Go relay server that bridges players to hosts |
| [website](https://github.com/VOXELPORT/website) | voxelport.in |

> The Fabric mod ([VoxelPort](https://github.com/VOXELPORT/VoxelPort)) opens the world or Fabric server you are already in to friends, with no account. For everything else (any server, modpacks, plugins, backups), use the app.

---

## Desktop App

An Electron app for Windows and Linux (macOS soon). There is also an **Android app** that hosts a server from your phone ([install guide](https://voxelport.in/guides/host-minecraft-server-android-phone), [source](https://github.com/VOXELPORT/voxelport-mobile)), with the same Discord sign-in and address backup.

- **New server:** pick Vanilla, Paper or Fabric and a version — VoxelPort downloads it and starts it.
- **Your server:** import an existing server folder, or tunnel one that's already running on any port.
- **Java handled for you:** the correct Eclipse Temurin version is downloaded and checksum-verified automatically, including Java 25 for Minecraft 26.1+.
- **Live console**, player count and relay ping, a RAM slider sized to your PC, and server files on any drive.
- **Direct routing:** connects straight to the relay for low ping, falling back to Cloudflare if a network blocks it.
- **Discord sign-in:** hosts sign in with Discord once and join our server. VoxelPort never sees your Discord password or email, and friends who only play never sign in.
- **Address backup:** lock your address with a passphrase and save it to your Discord account, then restore it on a new PC or phone. VoxelPort cannot read the backup or recover a forgotten passphrase.

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

Check live status on the [VoxelPort status page](https://voxelport.in/status). Need help? Open a ticket in our [Discord](https://discord.gg/JAUfmey2fP).

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
