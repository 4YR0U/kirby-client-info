# Kirby Client

Kirby Client is a small Minecraft 1.8.9 proxy written in Node.js, made by two friends for their own use on Hypixel (mainly Duels, also Bed Wars and SkyWars).

The game connects to the proxy on `localhost`, and the proxy relays everything to Hypixel while adding a few quality-of-life features in the chat, tab list and scoreboard.

**This repository only describes the project. It does not contain the source code.**

## Why the code is not here

The source code lives in a private repository. It is not public because:

- the proxy is only used by the two of us and is not meant to be distributed;
- we don't want people downloading it and running a proxy they don't understand on their Minecraft account.

**If you need to review the source code (for example as part of an API key application), just ask and I will send it to you.** You can open an issue on this repository to contact me.

## Commands that use the Hypixel API

If no player name is given, each command shows our own data.

| Command | What it does |
|---|---|
| `/ds [player] [mode]` | Shows a player's Duels stats (wins, losses, W/L ratio, winstreak, division), overall or for one mode. Also works for Bed Wars and SkyWars (`/ds bw`, `/ds sw`). |
| `/status [player]` | Shows which game, mode and map a player is currently in, and for how long. |
| `/guild [player]` | Shows a player's guild: name, tag, the player's rank in it, guild level and member count. |
| `/div [player]` | Shows a player's Duels division overall and in each mode, with the wins needed for the next one. |
| `/session` | Shows our own session stats (wins, losses, winstreak, wins per hour) since the session was started. |

## In-game display

- **Start of a game:** the stats of the players in the game are shown in the chat, in the tab list and above their heads.
- **Session scoreboard:** in Duels lobbies, a scoreboard shows our own stats for the current session. Wins and losses are counted from the game messages; our own profile is read a few times in the minute after a game to confirm the result.
- **Discord status:** our own stats can be shown in our Discord status. Our profile is read when we change server, and at most once every 3 minutes.

## How it uses the API

| Endpoint | Used for |
|---|---|
| `/v2/player` | Stats shown at the start of a game, `/ds`, `/div`, the session scoreboard and the Discord status |
| `/v2/status`, `/v2/recentgames` | `/status` |
| `/v2/guild` | `/guild` |

- Requests are only made when a game starts, when we type a command, or for our own profile as described above. There is no background tracking of other players.
- Responses are cached locally to keep the number of requests low.
- The API key is stored in a local config file on each user's computer. It is never written in the source code and never shared: each user enters their own key.

The proxy also has small features that don't use the API (sounds, ping display, settings profiles).

## Other

- Not monetized, not sold, not distributed publicly.
- Not affiliated with or endorsed by Hypixel.
