import GameHero from '@site/src/components/GameHero';

<GameHero
  title="Enshrouded"
  description="Connect Enshrouded dedicated servers to Takaro with one DLL: player events, chat, item delivery, teleports, and moderation."
  image="/img/games/enshrouded.jpg"
/>

Takaro supports Enshrouded through the Takaro Enshrouded Connector, a single `dbghelp.dll` that runs inside your dedicated server and implements the Takaro Generic Connector Protocol. Players do not install anything.

The connector connects outbound to Takaro over WebSocket, so no port forwarding is needed. Enshrouded has no RCON or console of its own; the connector provides player events, chat, item delivery, teleports, kick and ban.

## Installation

1. Download `takaro-enshrouded-plugin.zip` from the latest `enshrouded-vX.Y.Z` release (not a pre-release) on the [gettakaro/connectors releases](https://github.com/gettakaro/connectors/releases) page.
2. Stop your Enshrouded server and copy `dbghelp.dll` from the zip next to `enshrouded_server.exe`.
3. In Takaro, go to **Game servers**, click **Create new game server** and choose **Generic** to see your registration token. You do not need to create the server yourself; it appears in Takaro when it connects.
4. Start the server. It creates `takaro/plugin.json` next to `enshrouded_server.exe`; paste your registration token into `registrationToken` and save. The connector connects within a few seconds, no restart needed.

## Notes

- The connector is built for specific game builds. Releases up to v0.7.0 support game build 1024233; Enshrouded 1.0 support ships in the next release. Turn off automatic game updates so the server stays on a supported build.
- On Linux under Wine/Proton, set `WINEDLLOVERRIDES=dbghelp=n,b` so the server loads the connector.
- Enshrouded has no server sender for chat, so messages from Takaro appear under the name of an online player.

For setup details, Docker instructions and the full list of what works, see the [connector README](https://github.com/gettakaro/connectors/tree/main/games/enshrouded). For a high-level overview of how Takaro connects to game servers, see [Connection Architecture](/advanced/connection-architecture).
