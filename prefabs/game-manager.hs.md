### Game Manager

Manages general game events. Initialization on Match Start, Starting the game
on Round Start, clearing all the things, and sending the heartbeat.

---
###### Scripts

---
| #1 | Match Start|
| ---| ---|
|| `POWER` **Game -> Off**|
|| `SEND` **Reset**|

| #2 | Round Start| `Round Interrupt` `Always Run`|
| ---| ---| ---|
|| `POWER` **Game -> On**|

| #3 | `POWER` Game -> Off `OR` `SEND` Reset ||
| ---| ---| ---|
|| `NAV` **+Players**| `REMOVE` **+Nothing**|
|| `CLEAR TRAITS` **+Players**|
|| `SET FX` **+Players**| `FILTER`  **Default** `FX` **Default**|
|| `DESPAWN` **+This -Groups**|

| #4 | `POWER` Game -> On| `Round Interrupt` `Always Run`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #5 | `TIMER` Every 0.1| `Round Interrupt`|
| ---| ---| ---|
|| `SEND` **Heartbeat**|
