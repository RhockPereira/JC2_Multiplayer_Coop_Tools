# duo_supermod

> [!IMPORTANT]
> **RENAME `default_config.lua` TO `config.lua` IN THE JC2-MP DEDICATED SERVER FOLDER BEFORE STARTING THE SERVER.**
>
> Some installations may already include `config.lua`. If it already exists, do not overwrite it unless you know what you are changing.

## About

**duo_supermod** is an open-source co-op utility mod for **Just Cause 2 Multiplayer (JC2-MP)**.

The project was created with a simple idea: make private two-player sessions easier, faster and more fun without turning the server into a large or complicated gamemode.

It provides useful commands for:

* changing player skins;
* spawning personal vehicles;
* teleporting to your duo partner;
* bringing your duo partner to you;
* checking your duo's online status and distance;
* locating your duo partner;
* displaying a small client-side HUD with useful commands.

The project is intentionally lightweight and is aimed mainly at small private co-op sessions.

## Open Source

**duo_supermod is open source.**

You are free to:

* study the code;
* modify it;
* add new commands;
* change vehicle or character IDs;
* improve the HUD;
* adapt it for your own JC2-MP server;
* redistribute your own modified version.

Contributions, fixes and improvements are welcome.

If you redistribute a modified version, keeping a reference to the original project is appreciated.

## How It Works

Only the **host** needs to run the **Just Cause 2 Multiplayer Dedicated Server**.

The host runs:

```text
Just Cause 2 - Multiplayer Dedicated Server
└── JcmpServer.exe
```

and installs `duo_supermod` inside the Dedicated Server's `scripts` directory:

```text
Just Cause 2 - Multiplayer Dedicated Server/
├── JcmpServer.exe
├── config.lua
└── scripts/
    └── duo_supermod/
        ├── module.json
        ├── server/
        │   └── script.lua
        └── client/
            └── script.lua
```

The second player does **not** need to run another Dedicated Server.

JC2-MP automatically sends the module's required client-side scripts when a player connects to the server.

## Network Connection

The players must have a network path to the host's Dedicated Server.

For a simple private co-op setup, **Hamachi is recommended** because it creates a virtual LAN between the players.

```text
HOST
├── Just Cause 2
├── JC2-MP
├── JC2-MP Dedicated Server
└── Hamachi
        │
        │ Virtual LAN
        │
        ▼
PLAYER 2
├── Just Cause 2
├── JC2-MP
└── Hamachi
```

### Using Hamachi

1. The host creates or joins a Hamachi network.
2. Player 2 joins the same Hamachi network.
3. The host starts `JcmpServer.exe`.
4. Player 2 connects using the host's Hamachi IPv4 address and the port configured in `config.lua`.

> Hamachi is **not a dependency of duo_supermod itself**. It is simply an easy way to make the host reachable over a virtual LAN.

You can also use normal LAN networking, port forwarding, another VPN/VLAN solution, or a publicly reachable server.

## Installation

### 1. Install the JC2-MP Dedicated Server

Install **Just Cause 2: Multiplayer - Dedicated Server** using Steam or SteamCMD.

### 2. Configure the Dedicated Server

If your Dedicated Server contains:

```text
default_config.lua
```

rename or copy it to:

```text
config.lua
```

Then open `config.lua` and configure the server name, port and any other settings you want.

### 3. Install duo_supermod

Place the entire `duo_supermod` folder inside:

```text
Just Cause 2 - Multiplayer Dedicated Server/scripts/
```

The final structure should look like this:

```text
scripts/
└── duo_supermod/
    ├── module.json
    ├── README.md
    ├── server/
    │   └── script.lua
    └── client/
        └── script.lua
```

There is no need for `__resource.lua`.

JC2-MP automatically loads Lua files from a module's `server`, `client` and `shared` directories.

### 4. Start the Server

Run:

```text
JcmpServer.exe
```

A successful startup should include:

```text
Server started up successfully
```

The duo_supermod startup messages should also appear in the server console.

## Commands

Use:

```text
/list
```

in-game to display the command list.

### General

```text
/list
/duohud
```

### Skins

```text
/skin
/skin default
/skin 1
/skin 2
/skin police
/skin gang
/skin id NUMBER
```

### Vehicles

```text
/vehicles
/bike
/heli
/plane
/car
/veh id NUMBER
```

### Duo

```text
/duo
/duo set NAME
/duo clear
/tpduo
/bringduo
/duostatus
/findduo
```

Some legacy Portuguese command aliases are still accepted internally for compatibility with older versions of the mod, but they are not shown in `/list`.

## Host Responsibilities

The host is responsible for:

* running `JcmpServer.exe`;
* keeping `duo_supermod` installed in the server;
* configuring `config.lua`;
* keeping the network connection available;
* sharing the server address with the other player.

## Player Requirements

The other player only needs:

* Just Cause 2;
* JC2-MP;
* network access to the host;
* Hamachi too, if the host is using Hamachi.

The other player does **not** need to manually install `duo_supermod` or run the Dedicated Server.

## Project Structure

```text
duo_supermod/
├── module.json
├── README.md
├── server/
│   └── script.lua
└── client/
    └── script.lua
```

## Notes

This project targets **JC2-MP 0.3.x** and is designed mainly for small private co-op sessions.

Vehicle and character IDs can be changed directly in `server/script.lua`.

If something does not work, check the Dedicated Server console first. `duo_supermod` prints startup and error information there.

---

**Have fun causing chaos together.**
