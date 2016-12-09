# Universal Variable Chart

|              | Message | Power  | Global #      | Team #        | Player#       | Label         | Trait    |
| ---:         | :---:   | :---:  | :---:         | :---:         | :---:         | :---:         | :---:    |
| **Alpha**    |         |        | {ALIVE}       |               | {ALIVE}       |               | {ACTIVE} |
| **Bravo**    |         |        |               |               |               |               |          |
| **Charlie**  |         |        | {COLLECATBLE} | {COLLECTABLE} | {COLLECTABLE} | {COLLECTABLE} |          |
| **Delta**    |         |        | {DEAD}        |               | {DEAD}        |               |          |
| **Echo**     |         |        |               |               |               |               |          |
| **Foxtrot**  |         |        |               |               |               |               |          |
| **Golf**     |         | {GAME} |               |               |               |               |          |
| **Hotel**    |         |        |               |               |               |               |          |
| **India**    |         |        |               |               |               |               |          |
| **Juliet**   |         |        |               |               |               |               |          |
| **Kilo**     |         |        |               |               |               |               |          |
| **Lima**     |         |        |               |               |               |               |          |
| **Mike**     |         |        |               |               |               |               |          |
| **November** |         |        |               |               |               |               |          |
| **Oscar**    |         |        |               |               |               |               |          |
| **Papa**     |         |        | {PLAYER}      |               | {PLAYER}      |               |          |
| **Quebec**   |         |        |               |               |               |               |          |
| **Romeo**    | {RESET} |        |               |               |               |               |          |
| **Sierra**   |         |        |               |               |               |               |          |
| **Tango**    |         |        | {TEAM}        |               | {TEAM}        |               |          |
| **Uniform**  |         |        |               |               |               |               |          |
| **Victor**   |         |        |               |               |               |               |          |
| **Whiskey**  |         |        |               |               |               |               |          |
| **Xray**     |         |        |               |               |               | {UI}          |          |
| **Yankee**   |         |        |               |               |               |               |          |
| **Zulu**     |         |        |               |               |               |               |          |


## Variable Explanations

The explanation of every variable in the chart sorted per category. The
checkboxes on the left designate whether that variable has supporting dev tools.

### Message
 - [ ] **{RESET}** - Reset the state of everything


### Power
 - [ ] **{GAME}** - Whether or not the Game is being played


### Global #
 - [ ] **{ALIVE}** - The count of all alive players
 - [ ] **{COLLECTABLE}** - The count of all collectables
 - [ ] **{DEAD}** - The count of all dead players
 - [ ] **{PLAYER}** - The count of all players
 - [ ] **{TEAM}** - The count of all teams


### Team #
 - [ ] **{COLLECTABLE}** - The count of all collectables owned by the team


### Player #
 - [ ] **{ALIVE}** - The index of the player among all alive players
 - [ ] **{COLLECTABLE}** - The count of all collectables the player has
 - [ ] **{DEAD}** - The index of the player among all dead players
 - [ ] **{PLAYER}** - The index of the player among all players
 - [ ] **{TEAM}** - The index of the player among all teammates


### Label
 - [ ] **{COLLECTABLE}** - These objects can be picked up by players and despawn when they are
 - [ ] **{UI}** - These objects offset the player to be a binding point for UI elements

### Trait
 - [ ] **{ACTIVE}** - The currently active player
