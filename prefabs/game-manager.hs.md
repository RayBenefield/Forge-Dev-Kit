# Game Manager

Manages general game events. Initialization on Match Start, Starting the game
on Round Start, clearing all the things, and sending the heartbeat.

## Configuration

### Messages Memory

###### `INDIA` - Initialize

This is run on Match start.

###### `HOTEL` - Heartbeat

This is a synchronized Heartbeat every .1 seconds. It is used to handle event
loop tasks.

### Power Memory

###### `GOLF` - Game

If this is on then the Game is being played. If it is turned off, then the
Game has ended.


### Global \# Memory

###### `VICTOR` - Volatile

This is a temporary memory location for Forge math.


## Scripts

| #1 | Match Start|
| ---| ---|
|| `POWER` **Game -> Off**|
|| `SEND` **Initialize**|

| #2 | `HEAR` Initialize|
| ---| ---|
|| `CHANGE` **Volatile**| `SET` 0|

| #3 | Round Start| `Round Interrupt` `Always Run`|
| ---| ---| ---|
|| `POWER` **Game -> On**|

| #4 | `POWER` Game -> Off `OR` `HEAR` Initialize ||
| ---| ---| ---|
|| `NAV` **+Players**| `REMOVE` **+Nothing**|
|| `CLEAR TRAITS` **+Players**|
|| `SET FX` **+Players**| `FILTER`  **Default** `FX` **Default**|
|| `DESPAWN` **+This -Groups**|

| #5 | `POWER` Game -> On| `Round Interrupt` `Always Run`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #6 | `TIMER` Every 0.1| `Round Interrupt`|
| ---| ---| ---|
|| `SEND` **Heartbeat**|
