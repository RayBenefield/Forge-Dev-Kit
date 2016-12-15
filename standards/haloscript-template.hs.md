## Setup System

The Setup System does things. This is a WIP progress proposed markdown template
for sharing scripting with the community.

### Setup Object

This is an example of an object in this collection. There could be many of
these and we need a way to display relevant object attributes.
- CONFIG [Cost of Cache] Add a (Message [X]) script for every unit of cost

---
###### Scripts

---

> Prepare to remove weapons on cache one Match Start

| #1 | RECEIVED {SCORE}|||
| ---| ---| ---| ---|
|| `NAV` **+Players -Dead**| `ADD` **+[HILL] -[TEAM 1] -[TEAM 2]**| `COLOR` **CONTESTED**|
|| `NAV` **+Players -Dead +[TEAM 1]**| `ADD` **+[HILL] -[TEAM 2]**| <li>`COLOR` **TEAM 2** <li>`SAY` **Attack**|
|| `WAIT` **1.0**|
|| `SEND` **Score**| `TRANSFER` **This**|

> TODO [Change to Round Start]

| #2 | RECEIVED {SCORE}||
| ---| ---| ---|
|| `ROUND` **3.00**|
|| `CHANGE` **Global# -> Max Hills**| `EQUALS`  **Game Value ->  Spawn Order**|
|| `CHANGE` **Team# -> Alive**| `EQUALS`  **Player# -> Spawn Order**|
|| `CHANGE` **Team$**| `EQUALS`  **Team# -> Alive**|

> Prepare to remove weapons on cache one Match Start
> TODO [Change to Round Start]

| #3 | RECEIVED {SCORE}|||
| ---| ---| ---| ---|
|| `CHANGE` **Player$**| `FILTER` **+Players** **+ThisTeam** **-Dead**| `EQUALS`  **Player# -> Alive**|
|| `POWER` **GAME** -> ON|

