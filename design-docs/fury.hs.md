# Fury

*<sub>Courtesy of Nitro, the Designer of Fury</sub>*

Fury is a multi-round scenario based game, intended for the players who want a
quick 10 min plus warmup game. For two minutes, you play one round in a room
filled with various height variations, line of sight blockers, standard weapons
and everything else that you would expect in a normal map. This room can
support both 1v1 and 2v2 gameplay. The team with the most kills wins the round.
After the round is complete however, you are spawned into a new room with
different height variations, routes, and weapons. Giving you the chance to win
the next round, after losing the last. This goes on until one team reaches 5
wins.

## Map Setup

1. **DOWNLOAD:** [FDK Fury
   Prefab](https://www.halowaypoint.com/en-us/games/halo-5-guardians/xbox-one/forge-object-groups?lastModifiedFilter=Everything&sortOrder=BookmarkCount&page=1&gamertag=Ray%20Benefield#ugc_halo-5-guardians_xbox-one_forgeobject_Ray%20Benefield_990dee6f-1d8e-4a77-8967-56f1481e2d54)
1. **PLACE** [FDK Fury
   Prefab](https://www.halowaypoint.com/en-us/games/halo-5-guardians/xbox-one/forge-object-groups?lastModifiedFilter=Everything&sortOrder=BookmarkCount&page=1&gamertag=Ray%20Benefield#ugc_halo-5-guardians_xbox-one_forgeobject_Ray%20Benefield_990dee6f-1d8e-4a77-8967-56f1481e2d54)
on your map
1. **CHANGE** The **Spawn Order** on the **MIDDLE** Script Brain to the number
   of areas/rounds on your map. This controls when **Fury** cycles rounds. For
example, if the **Spawn Order** is set to **[7]** (default), when Round 7 ends,
it will move to the first map for Round 8.
1. **SET** The **Spawn Order** for all spawns in a single area to the number
   round it is for. For example, the every spawn in the first round map should
be set to **[1]**, every spawn in the second round map should be set to
**[2]**, etc.

## FDK Components

### [Game Manager](../../prefabs/game-manager.hs.md)

Manages general game events. Initialization on Match Start, Starting the game
on Round Start, clearing all the things, and sending the heartbeat.

###### Condensed Scripts

| #1 | Match Start|
| ---| ---|
|| `SEND` **Initialize**|

| #2 | `HEAR` Initialize|
| ---| ---|
|| `CHANGE` **Volatile**| `SET` 0|


### [Round Manager](../../prefabs/round-manager.hs.md)

Manages all round tracking including a relative round based on spawn order. Set
the **Spawn Order** on this object to determine when the relative round cycles.
For example, if the **Spawn Order** is to 3, the **Current-Round** will be set
to 0 -> 1 -> 2 -> 0 -> 1... etc.

###### Condensed Scripts

| #1 | `HEAR` Initialize| |
| ---| ---:| :---|
|| `CHANGE` **Round-Number**| `SET` 0|
|| `CHANGE` **Current-Round**| `SET` 0|

| #2 | `ROUND START`|
| ---| ---:|
|| `POWER` **Round-Active -> On**|

| #3 | `ROUND TIME` 0.00|
| ---| ---:|
|| `CHANGE` **Round-Active -> Off**|

| #4 | `POWER` Round-Active -> Off| |
| ---| ---:| :---|
|| `CHANGE` **Round-Number**| `INCREMENT`|
|| `CHANGE` **Volatile**| `SET` **Round**|
|| `CHANGE` **Volatile**| `REMAINDER` **Game Value -> `THIS` Spawn Order**|
|| `CHANGE` **Current Round**| `SET` **Volatile**|

### [Round Spawner](../../prefabs/round-spawner.hs.md)

Progresses the Spawn Order of ALL players between 1 and the `Round Manager`
**Spawn Order** every single round. Round 1 **Spawn Order** is 1, Round 2
**Spawn Order** is 2, etc.  This allows developers to create maps that happen
in different locations in each round.

###### Condensed Scripts

| #1 | `HEAR` Initialize| |
| ---| ---:| :---|
|| `ORDER CHANGE` **+Players**| `SET` **1**|

| #2 | `CHECK` Current-Round > -1| |
| ---| ---:| :---|
|| `ORDER CHANGE` **+Players**| `SET` **Current-Round + 1**|
