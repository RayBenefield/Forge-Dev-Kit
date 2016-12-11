# Round Sequencer

Progresses the Spawn Order of ALL players between 1 and `THIS` **Spawn Order**
every single round. Round 1 **Spawn Order** is 1, Round 2 **Spawn Order** is 2, etc.
This allows developers to create maps that happen in different locations in
each round.

## Configuration

### Global \# Memory

###### `ROMEO` - Round

Zero-indexed (like programming). Round 1 is 0, Round 2 is 1, Round 3 is 2, etc.

###### `CHARLIE` - Current-Round

Zero-indexed (like programming). Set as the Remainder of {ROUND} and the Spawn
Order of the sequencer (default to 7 thanks to Fury). This results in numbers
between `0` to `Spawn Order - 1`

###### `VICTOR` - Volatile

This is a temporary memory location for Forge math.


### Spawn Order

###### `THIS`

The spawn order for this designates the number of rounds/locations that you
have. For example if you have 3 locations this will be set to 3 and every
player will spawn on spawn points that match spawn order 1 in round 1, spawn
order 2 in round 2, etc. After the third round it will reset back to 1 and
continue.

###### All Players

The spawn orders for all players are automatically set to the
**Current-Round**. This forces players to spawn in the given location based on
what round they are on.


## Scripts

| #1 | `MATCH START`| |
| ---| ---:| :---|
|| `CHANGE` **Round**| `SET` 0|
|| `CHANGE` **Current-Round**| `SET` 0|
|| `CHANGE` **Volatile**| `SET` 0|
|| `ORDER CHANGE` **+Players**| `SET` **1**|

| #2 | `ROUND TIME` 0.00| |
| ---| ---:| :---|
|| `CHANGE` **Round**| `INCREMENT`|
|| `CHANGE` **Volatile**| `SET` **Round**|
|| `CHANGE` **Volatile**| `REMAINDER` **Game Value -> `THIS` Spawn Order**|
|| `CHANGE` **Current Round**| `SET` **Volatile**|

| #3 | `CHECK` Current-Round > -1| |
| ---| ---:| :---|
|| `ORDER CHANGE` **+Players**| `SET` **Current-Round + 1**|
