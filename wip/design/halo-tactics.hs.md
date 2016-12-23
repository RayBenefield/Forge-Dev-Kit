## Planning


### Data Needed

 - Global
     - Cumulative Turns
     - Cumulative Rounds
     - Relative Turn
     - Turn Length
     - Round Length (Number of Turns based on the largest team count)
     - [ Round Limit ]
     - [ Turn Limit ]
 - Player
     - Player Team ID

```
if (PlayerTeamID === RelativeTurn) {
    player.getActiveAspect
} else {
    player.clearAspects
}

if (PlayerDies) {
    if (
        DeadPlayerID NotLastInTurnOrder
        && EndOfRound
    ) {
        ChangePlayerID of every Player after DeadPlayer
        UpdatedMaxTeamSize
    }

    if (MaxTeamSize Changes) {
        Reduce the Round Length to the new MaxTeamSize
    }
}
```

### Turn Simulation Table

| Rd  | Cum | Rel | T0 Sz | T0 P0   | T0 P1   | T0 P2   | T0 P3   | T1 Sz | T1 P0   | T1 P1   | T1 P2   | T1 P3   |
| --- | --- | --- | ---   | ---     | ---     | ---     | ---     | ---   | ---     | ---     | ---     | ---     |
| 0   | 0   | 0   | 4     | **[0]** | 1       | 2       | 3       | 4     | **[0]** | 1       | 2       | 3       |
| 0   | 1   | 1   | 4     | 0       | **[1]** | 2       | 3       | 4     | 0       | **[1]** | 2       | 3       |
| 0   | 2   | 2   | 4     | 0       | 1       | **[2]** | 3       | 4     | 0       | 1       | **[2]** | 3       |
| 0   | 3   | 3   | 4     | 0       | 1       | 2       | **[3]** | 4     | 0       | 1       | 2       | **[3]** |
| 1   | 4   | 0   | 4     | **[0]** | 1       | 2       | 3       | 4     | **[0]** | 1       | 2       | 3       |
| 1   | 5   | 1   | 4     | 0       | **[1]** | 2       | 3       | 4     | 0       | **[1]** | 2       | 3       |
| 1   | 6   | 2   | 4     | 0       | 1       | **[2]** | 3       | 4     | 0       | 1       | **[2]** | 3       |
| 1   | 7   | 3   | 4     | 0       | 1       | 2       | **[3]** | 4     | 0       | 1       | 2       | **[3]** |
| 2   | 8   | 0   | 3     | **[0]** | **[x]** | 1       | 2       | 4     | **[0]** | 1       | 2       | 3       |
| 2   | 9   | 1   | 3     | 0       | **[x]** | **[1]** | 2       | 4     | 0       | **[1]** | 2       | 3       |
| 2   | 10  | 2   | 3     | 0       | **[x]** | 1       | **[2]** | 4     | 0       | 1       | **[2]** | 3       |
| 2   | 11  | 3   | 3     | 0       | **[x]** | 1       | 2       | 4     | 0       | 1       | 2       | **[3]** |
| 3   | 12  | 0   | 3     | **[0]** | **[x]** | 1       | 2       | 4     | **[0]** | 1       | 2       | 3       |
| 3   | 13  | 1   | 3     | 0       | **[x]** | **[1]** | 2       | 4     | 0       | **[1]** | 2       | 3       |
| 3   | 14  | 2   | 3     | 0       | **[x]** | 1       | **[2]** | 4     | 0       | 1       | **[2]** | 3       |
| 3   | 15  | 3   | 3     | 0       | **[x]** | 1       | 2       | 4     | 0       | 1       | 2       | **[3]** |
| 4   | 16  | 0   | 2     | **[0]** | **[x]** | 1       | **[x]** | 4     | **[0]** | 1       | 2       | 3       |
| 4   | 17  | 1   | 2     | 0       | **[x]** | **[1]** | **[x]** | 3     | 0       | **[1]** | **[x]** | 2       |
| 4   | 18  | 2   | 2     | 0       | **[x]** | 1       | **[x]** | 3     | 0       | 1       | **[x]** | **[2]** |
| 5   | 19  | 0   | 2     | **[0]** | **[x]** | 1       | **[x]** | 2     | **[0]** | 1       | **[x]** | **[x]** |
| 5   | 20  | 1   | 2     | 0       | **[x]** | **[1]** | **[x]** | 2     | 0       | **[1]** | **[x]** | **[x]** |
| 6   | 21  | 0   | 2     | **[0]** | **[x]** | 1       | **[x]** | 2     | **[0]** | 1       | **[x]** | **[x]** |
| 6   | 22  | 1   | 2     | 0       | **[x]** | **[1]** | **[x]** | 2     | 0       | **[1]** | **[x]** | **[x]** |
| 7   | 23  | 0   | 2     | **[0]** | **[x]** | 1       | **[x]** | 2     | **[0]** | 1       | **[x]** | **[x]** |
| 7   | 24  | 1   | 2     | 0       | **[x]** | **[1]** | **[x]** | 2     | 0       | **[1]** | **[x]** | **[x]** |

## Memory Chart

|              | Message      | Power          | Global #        | Team # | Player# | Label | Aspect   |
| ---:         | :---:        | :---:          | :---:           | :---:  | :---:   | :---: | :---:   |
| **Alpha**    |              |                |                 |        |         |       |         |
| **Bravo**    |              |                |                 |        |         |       |         |
| **Charlie**  |              |                | Current-Turn    |        |         |       |         |
| **Delta**    |              |                |                 |        |         |       | Dormant |
| **Echo**     |              |                |                 |        |         |       |         |
| **Foxtrot**  |              |                |                 |        |         |       |         |
| **Golf**     |              | Game-Active    |                 |        |         |       |         |
| **Hotel**    | {HEARTBEAT}  |                |                 |        |         |       |         |
| **India**    | {INITIALIZE} |                |                 |        |         |       |         |
| **Juliet**   |              |                |                 |        |         |       |         |
| **Kilo**     |              |                |                 |        |         |       |         |
| **Lima**     |              |                |                 |        |         |       |         |
| **Mike**     |              |                | {MAX-TEAM-SIZE} |        |         |       |         |
| **November** |              |                |                 |        |         |       |         |
| **Oscar**    |              |                |                 |        | {ORDER} |       |         |
| **Papa**     |              |                |                 |        |         |       |         |
| **Quebec**   |              |                |                 |        |         |       |         |
| **Romeo**    | {ROUND-INIT} | {ROUND-ACTIVE} | {ROUND-NUMBER}  |        |         |       |         |
| **Sierra**   |              |                |                 | {SIZE} |         |       |         |
| **Tango**    | {TURN-START} | {TURN-ACTIVE}  | {TURN-NUMBER}   |        |         |       |         |
| **Uniform**  |              |                |                 |        |         |       |         |
| **Victor**   |              | {VOLATILE}     |                 |        |         |       |         |
| **Whiskey**  |              |                |                 |        |         |       |         |
| **Xray**     |              |                |                 |        |         |       |         |
| **Yankee**   |              |                |                 |        |         |       |         |
| **Zulu**     |              |                |                 |        |         |       |         |

## Components

### Game Manager

Manages general game events. Initialization on Match Start, Starting the game
on Round Start, clearing all the things, and sending the heartbeat.

---
###### Scripts

| #1 | Match Start|
| ---| ---|
|| `POWER` **Game -> Off**|
|| `SEND` **Initialize**|

| #2 | Round Start| `Round Interrupt` `Always Run`|
| ---| ---| ---|
|| `POWER` **Game -> On**|

| #3 | `POWER` Game -> Off `OR` `HEAR` Initialize ||
| ---| ---| ---|
|| `NAV` **+Players**| `REMOVE` **+Nothing**|
|| `CLEAR TRAITS` **+Players**|
|| `SET FX` **+Players**| `FILTER`  **Default** `FX` **Default**|
|| `DESPAWN` **+This -GroupSiblings**|

| #4 | `POWER` Game -> On| `Round Interrupt` `Always Run`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #5 | `TIMER` Every 0.1| `Round Interrupt`|
| ---| ---| ---|
|| `SEND` **Heartbeat**|

---

### Turn Manager

Manages the Turn taking system.

---
###### Scripts

| #1 | `TIMER` Every 4.00| `Round Interrupt`|
| ---| ---| ---|
|| `SEND` **Turn-Start**|

| #2 | `POWER` Game -> On| `Round Interrupt` `Always Run`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #3 | `POWER` Game -> Off `OR` `HEAR` Initialize ||
| ---| ---| ---|
|| `CHANGE` **Turn-Number**| `SET` **-1**|
|| `CHANGE` **Current-Turn**| `SET` **-1**|
|| `DESPAWN` **+This -GroupSiblings**|

| #4 | `HEAR` Turn-Start||
| ---| ---| ---|
|| `CHANGE` **Turn-Number**| `INCREMENT`|
|| `CHANGE` **Volatile**| `SET` **Turn-Number**|
|| `CHANGE` **Volatile**| `REMAINDER` **Max-Team-Size**|
|| `CHANGE` **Current-Turn**| `SET` **Volatile**|

---

### Team Manager

Manages the Teams in the game.

---
###### Scripts

> - On Initialize set the Max-Team-Size to -1

### Player Manager

Manages the Players in the game.

---
###### Scripts

> - If My Turn then set as Active
> - If Not My Turn then Remove Active Aspect

| #1| `CHECK` Max-Team-Size > 0||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **25**|
|| `CHANGE` **This**| `SET` **1**|

| #2| `CHECK` This < Max-TeamSize||
| ---| ---| ---|
|| `ORDER CHANGE` **+Players +This.Team +Order[0] +Random[1]**| `SET` **This**|
|| `CHANGE` **This**| `INCREMENT`|

| #3| `CHECK` Current-Turn > -1||
| ---| ---| ---|
|| `ORDER CHANGE` **This**| `SET` **Current-Turn**|
|| `APPLY TRAIT` **+Players -This.Order**| `SET` **Dormant**|
|| `CLEAR TRAITS` **+Players +This.Order**|

| #4| `CHECK` Current-Turn > -1||
| ---| ---| ---|
|| `ORDER CHANGE` **This**| `SET` **Current-Turn**|
|| `NAV` **+Players +This.Team**| `TARGET` **+Players +This.Order**| `COLOR` **Active** `SAY` **Active**|
|| `CLEAR NAV` **+Players +This.Team**| `TARGET` **+Players +This.Order**|

---
