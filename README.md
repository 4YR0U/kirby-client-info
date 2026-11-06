# Kirby Client

Kirby Client is a small Minecraft 1.8.9 proxy written in Node.js, made by two friends for their own use on Hypixel (mainly Duels, also Bed Wars and SkyWars).

The game connects to the proxy on `localhost`, and the proxy relays everything to Hypixel while adding a few quality-of-life features in the chat, tab list and scoreboard.

**This repository only describes the project. It does not contain the source code.**

## Why the code is not here

The source code lives in a private repository. It is not public because:

- the proxy is only used by the two of us and is not meant to be distributed;
- we don't want people downloading it and running a proxy they don't understand on their Minecraft account.

**If you need to review the source code (for example as part of an API key application), just ask and I will send it to you.** You can open an issue on this repository to contact me.

## How it uses the Hypixel Public API

The proxy calls the API only when a game starts or when we type a command:

| Endpoint | Used for |
|---|---|
| `/v2/player` | Stats of the players in our current game (Duels, Bed Wars, SkyWars), and the `/ds <player>` command |
| `/v2/status`, `/v2/recentgames` | The `/status <player>` command (which game a player is in) |
| `/v2/guild` | The `/guild <player>` command |

It also reads our own profile once after a game, to keep a local session counter (wins / losses) correct.

- No background polling, no tracking of other players over time.
- Responses are cached locally to keep the number of requests low.
- The API key is stored in a local config file on each user's computer. It is never written in the source code and never shared: each user enters their own key.

## Other

- Not monetized, not sold, not distributed publicly.
- Not affiliated with or endorsed by Hypixel.
