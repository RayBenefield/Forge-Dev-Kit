# Stockpile

<sub>Courtesy of Max Extra</sub>

## General Suggestions

 - Countdown timer for scoring
 - Individual player scoring (Perhaps use the Object scoped local variable to
   store an index for the last player to touch it)

## Memory Suggestions

 - [Message] Suggest to change **November (Noises)** to **India (Initialize)**
     - Used in 343's KoTH and Fury
     - I don't see a real need for sounds to have their own event... they
       should be reactive based on actual events that happen, if we need a
sound for something then we should probably have some sort of event for that
 - [Power]Suggest to change **Sierra (Start)** to **Golf (Game)**
     - Used in 343's KoTH and Fury
     - The major name change reasoning for Game vs Start, is that a Power
       channel represents a continuous stream and Start is a singular event
     - In the FDK the **Game** channel starts on `Round Start` instead of
       `Match Start`, things that need to happen before the round starts, are
recommended to be done off of **Initialization**
 - [Message] Suggest to change **Alpha** to **Hotel (Heartbeat)**
     - Used in 343 KoTH, and I think it just makes more sense
 - [Message] Suggest to change **Charlie (Capture)** to **Sierra (Score)**
     - Makes it more generic for any scoring events for other gametypes
     - I think this should work well with Invasion considering that Invasion
       needs to score every second, or score when a flag enters a zone, or
score when a core is destroyed, strongholds needs a score every second, etc.
 - [Label] Maybe change **Foxtrot (Flag)** to **Oscar (Objective)** OR
   **Charlie (Collectable)**
     - We should consider Assault, Headhunter, CTF, Strongholds, KoTH (uses
       Hotel for Hill), Oddball
 - [Label] Keep **Zulu (Zone)**
     - This should be flexible enough for anything that uses boundaried areas;
       CTF, Assault, KoTH, Stockpile, Headhunter
 - [Label] Remove the **Quebec (Queued)** label
     - I actually don't think you need this label
     - Anywhere that you use the channel, it seems like you can just use the
       **Flag** label
     - When you add a navpoint for the **Queued** you don't need to add the
       label
     - When you score you can just score all **Flags** in the boundary instead
       of **Queued**
     - No need to remove the waypoint on the **Flag** on boundary enter
       (Pickup)
 - Move from using Global channels for each team... use a Team Scoped channel
   with **Sierra (Size)** OR **Papa (Players)** (We may want to use **Sierra
(Score)** for teams
     - I checked that team scoped variables work fine and size should work for
       other gametypes
     - This channel should be widely used on all gametypes to watch for when
       teams exist and don't
     - It should just be a matter of Number Check > 0, Scope Team, Team of the
       zone, **Sierra (Size)** to detect whether it should be spawned
     - And another check for all players on the team when it is <= 0, and as
       you said we need to count dead players, because otherwise an event would
trigger when all players are dead

I can't remember exactly how you are handling the number of flags, but it
looked like it was hard coded to around the number of 4. It should be possible
to set the spawn order on that script brain to manage the number of flags that
should be spawned at a time on that map. So perhaps on **Initialize** the
script brain sets a channel with the number of **Objectives** to have and then
all of its operations are done off of that number memory slot.


## Component Suggestions

### Game Manager

Manage the state of the game.

## Scripts

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
|| `DESPAWN` **+This -Groups**|

| #4 | `POWER` Game -> On| `Round Interrupt` `Always Run`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #5 | `TIMER` Every 0.1| `Round Interrupt`|
| ---| ---| ---|
|| `SEND` **Heartbeat**|


### Stockpile Manager

Manages how many flags need to be spawned and when.

 > - On **Game -> Off**, Despawn
 > - **Always Run** On **Game -> On**, Spawn
 > - On Timer Repeat 60, then **Score**
 > - When **Score** happens, then spawn enough flags to equal the spawn order of this


### Score Mangaer

Watches the designated score channels and updates scores:

 > - When Team **Score** changes, then set the Score for that team
 > - When Player **Score** changes, then set the Score for that player


### Team Manager

Updates Team properties on Heartbeat.

 > - On **Heartbeat**, Update **Size** of every team
 > - On **Size** > 0, Update **Exists** to positive number
 > - On **Size** <= 0, Update **Exists** to negative number


### Stockpile Zone

Captures all **Objectives** in the boundary.

 - Labels: **Zone**

 > - On **Team Exists** positive, Force Spawn
 > - On **Team Exists** negative, then Despawn this object
 > - On **Score**, count the **Objectives** in the boundary set into the **Team
 >   Score**, then despawn all **Objectives** in the boundary


### Flag

 - Labels: **Objective**

 > - On **Player Enter**, Remove Navpoint from all players
 > - On **Player Exit**, Add Navpoint to all players
