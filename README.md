# Stand-Ins

Place a server-side stand-in of yourself with `/stand-in`. A stand-in is a fake player
(like Carpet's `/player`) that wears your skin, has no name tag, is hidden from the
tab list and stays where you put it until it is killed.

## Commands

| Command | Who | What |
| --- | --- | --- |
| `/stand-in` or `/stand-in spawn` | everyone | Places a stand-in at your position (if you are below your limit). |
| `/stand-in spawn <name>` | everyone | Same, with a custom name (use quotes for spaces: `/stand-in spawn "Door guard"`). The name replaces the number in the tab list and messages. |
| `/stand-in list` | everyone* | Your stand-ins with position, distance and direction. |
| `/stand-in kill [number\|name\|all]` | everyone* | Removes your own stand-in(s). The number is the one from `list`. |
| `/stand-ins list` | ops (level 2) | Every stand-in on the server (owner, position, dimension). |
| `/stand-ins reload` | ops (level 2) | Reloads `config/stand-ins.json`. |

\* `list` and `kill` can each be switched off in the config.

A stand-in is also removed when it dies (no drops, no public death message). Its owner
gets the death message instead ("... was slain by Zombie", or "You killed your stand-in.").
If the owner is offline, the message is saved and shown when they join.

## Config (`config/stand-ins.json`, `//` comments allowed)

| Key | Default | Meaning |
| --- | --- | --- |
| `maxStandinsPerPlayer` | `1` | How many stand-ins one player may have at once (`0` disables placing). |
| `onlyCreatorCanKill` | `true` | Only the creator's attacks hurt the stand-in (mobs, lava and the void still can). Has no effect while `invulnerable` is on. |
| `disableCollisions` | `true` | Stand-ins are not pushed and do not push others (players and mobs walk through them). Water currents and pistons do not move them either. |
| `disableKnockback` | `true` | No knockback from hits, projectiles or explosions. |
| `hideFromTabList` | `true` | Stand-ins are not shown in the tab list for normal players. |
| `showInTabListForCreator` | `false` | The player who placed a stand-in also sees it in the tab list. |
| `enableListCommand` / `enableKillCommand` | `true` | Switch `/stand-in list` and `/stand-in kill` on or off. |
| `invulnerable` | `true` | Stand-ins cannot be hurt or killed by anything; only `/stand-in kill` removes them (stays available even if `enableKillCommand` is false). Overrides `onlyCreatorCanKill`. |
| `showInTabListForAdmins` | `true` | Operators (level 2+) still see them in the tab list, in gray italics, as `<player>'s standin` (numbered, e.g. `standin 2`, only if that player has several). |

## Behaviour

- Stand-ins are saved with the world and come back after a restart. The list lives in
  `<world>/stand-ins/standins.json`; each stand-in's position and dimension are saved there too.
- Empty inventory, no item or XP pickup, and no armor from dispensers.
- Like a real player they load chunks, count for mob spawning and are targeted by mobs.
- They are real players internally, so they match `@a` and show in `/list`, but they are hidden from the tab list and not counted in the server list player count.

## Requirements

Minecraft 26.3, Fabric Loader 0.20.1+, Java 25 and Fabric API. Install it on the server; in single-player it works as well.

## License

CC0 1.0 (public domain).
