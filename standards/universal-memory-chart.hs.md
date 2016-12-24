# Universal Memory Chart

In order to speed up development time I propose we create a universal standard
for memory usage to encourage re-usable components and a unified design
language. This chart is inspired by the 343 Design Documents, and follows their
idea of utilizing a naming conventions for each area of memory. Each concept
chooses a unique letter to tie to a respective channel. This is typically the
first letter of the concept, but may be other letters. This naming convention
makes complex systems much easier to follow.

If you would like to suggest a new universal allocation, then please put in an
[issue](https://github.com/RayBenefield/Forge-Dev-Kit/issues) so it can be
discussed amongst the community. An accepted proposal will either be added by a
contributor, or you can submit your own [pull
request](https://github.com/RayBenefield/Forge-Dev-Kit/pulls).

|              | Message        | Power        | Global #      | Team # | Player# | Label    | Trait |
| ---:         | :---:          | :---:        | :---:         | :---:  | :---:   | :---:    | :---: |
| **Alpha**    |                |              |               |        |         |          |       |
| **Bravo**    |                |              |               |        |         | Ball     |       |
| **Charlie**  |                |              | Current-Round |        |         | Child    |       |
| **Delta**    |                |              |               |        |         |          |       |
| **Echo**     | Enter-Boundary |              |               |        |         |          |       |
| **Foxtrot**  |                |              |               |        |         | Flag     |       |
| **Golf**     |                | Game-Active  |               |        |         | Gametype |       |
| **Hotel**    | Heartbeat      |              |               |        |         |          |       |
| **India**    | Initialize     |              |               |        |         | Invalid  |       |
| **Juliet**   |                |              |               |        |         |          |       |
| **Kilo**     |                |              |               |        |         |          |       |
| **Lima**     |                |              |               |        |         |          |       |
| **Mike**     |                |              |               |        |         | Mutator  |       |
| **November** |                |              |               |        |         |          |       |
| **Oscar**    |                |              |               |        |         |          |       |
| **Papa**     |                |              |               |        |         | Player   |       |
| **Quebec**   |                |              |               |        |         |          |       |
| **Romeo**    |                | Round-Active | Round-Number  |        |         | Rate     |       |
| **Sierra**   | Score          |              |               |        |         | Score    |       |
| **Tango**    | Tag-Team       |              |               |        |         | Team     |       |
| **Uniform**  |                |              |               |        |         |          |       |
| **Victor**   | Value          |              |               |        |         | Vehicle  |       |
| **Whiskey**  |                |              |               |        |         | Weapon   |       |
| **Xray**     | Exit-Boundary  |              |               |        |         |          |       |
| **Yankee**   |                |              |               |        |         |          |       |
| **Zulu**     |                |              |               |        |         | Zone     |       |


## Memory Explanations

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
