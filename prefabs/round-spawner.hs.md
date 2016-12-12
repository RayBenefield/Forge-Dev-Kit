# Round Spawner

Progresses the Spawn Order of ALL players between 1 and the `Round Manager`
**Spawn Order** every single round. Round 1 **Spawn Order** is 1, Round 2
**Spawn Order** is 2, etc.  This allows developers to create maps that happen
in different locations in each round.

## Configuration

### Messages Memory

###### `INDIA` - Initialize

This is run on Match start. We use this to default the spawn order of players to 1.


### Global \# Memory

###### `CHARLIE` - Current-Round

Zero-indexed (like programming). Set as the Remainder of **Round-Number** and
the Spawn Order of the sequencer (default to 7 thanks to Fury). This results in
numbers between `0` to `Spawn Order - 1`. We use this to determine


### Spawn Order

###### All Players

The spawn orders for all players are automatically set to the **Current-Round**
when it changes. This forces players to spawn in the given location based on
what round they are on.


## Scripts

| #1 | `HEAR` Initialize| |
| ---| ---:| :---|
|| `ORDER CHANGE` **+Players**| `SET` **1**|

| #2 | `CHECK` Current-Round > -1| |
| ---| ---:| :---|
|| `ORDER CHANGE` **+Players**| `SET` **Current-Round + 1**|
