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
    player.getActiveTrait
} else {
    player.clearTraits
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


## Components

### Game Manager

Manages general game events. Initialization on Match Start, Starting the game
on Round Start, clearing all the things, and sending the heartbeat.

---
###### [Scripts](../../prefabs/game-manager.hs.md)

---


### Turn Manager

Manages the Turn taking system.

---
###### Scripts

> - Set all turn trackers to 0
> - Initialize the Turn Length
> - Send a Turn Heartbeat every X amount of time

---

### Player Manager

Manages the Turn taking system.

---
###### Scripts

> - If My Turn then set as Active
> - If Not My Turn then Remove Active Trait

---
