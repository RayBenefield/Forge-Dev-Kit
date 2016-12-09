    # Manages pre-warming setup and despawning of weapon
    #  - CONFIG [Cost of Cache] Add a (Message [X]) script for every unit of cost
| Setup System
| ---
| [Any Invisible Scriptable Object]
    # Prepare to remove weapons on cache one Match Start
    # TODO [Change to Round Start]
| #1 | NAV MARKER: CHANGE
| ---|---|
||PLAYERS <li>Players [add]
||Add
||TARGETS <li>Label [add] {HILL} <li>Label [exclude] {TEAM 1} <li>Label [exclude] {TEAM 2}
||Color: {CONTESTED} 
||Text: <none\>

| #1 | RECEIVED {SCORE}||||
| ---|---|---|---|---|
||NAV **+Players -Dead**|ADD <li>**+[HILL]** <li>**-[TEAM 1]** <li>**-[TEAM 2]**|COLOR **CONTESTED**
||NAV <li>**+Players <li>-Dead <li>+[TEAM 1]**|ADD <li>**+[HILL]** <li>**-[TEAM 2]**|COLOR **TEAM 2**|SAY **Attack**
||WAIT **1.0**
||SEND **Score**|TRANSFER **This**
||ROUND **3.00**
||CHANGE **Global# -> Max Hills**|EQUALS  **Game Value ->  Spawn Order**
||CHANGE **Team# -> Alive**|EQUALS  **Player# -> Spawn Order**
||CHANGE **Team$**|EQUALS  **Team# -> Alive**
||CHANGE **Player$**|FILTER <li>**+Players** <li>**+ThisTeam** <li>**-Dead**|EQUALS  **Player# -> Alive**
||POWER **GAME** -> ON


---

Action #1

---

| Number: CHANGE|DESPAWN
|---|---
|Scope: Global|

| #2 | NUMBER: CHANGE
| ---|---|
||Scope: Global
||Channel: {MAX HILLS}
||Operation: Set
||Source: Game Value
||Game Value: Spawn: Order
||Randomize: Off

```
var MAX HILLS = "Source"
```

# Remove weapons from cache
2 (Timer [12.00])<Power [A=Off]>
# Pre-warm cache with resource
*[Cost of Cache] (Timer [#.##])<Message [A]>
{
    1 (Timer [1.00])<Power [B=On]>
    2 (Timer [12.00])<Power [B=Off]>
    *[Cost of Cache] (Timer [#.##])<Message [B]>
}
