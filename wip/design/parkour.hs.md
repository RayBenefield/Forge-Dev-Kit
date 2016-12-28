# Parkour

Parkour is a gametype that embodies the spirit and skill behind parkour. Here
is the definition from wikipedia:

> Parkour is a training discipline using movement that developed from military
> obstacle course training.  Practitioners aim to get from one point to another
> in a complex environment, without assistive equipment and in the fastest and
> most efficient way possible. Parkour includes running, climbing, swinging,
> vaulting, jumping, rolling, quadrupedal movement, and other movements as
> deemed most suitable for the situation. Parkour's development from military
> training gives it some aspects of a non-combative martial art.

In Halo this is akin to utilizing the spartan abilities to their maximum
capabilities. A new batch of settings have been constructed to add even more
possibilities for level traversal.


## Objective

In Parkour maps there are X amount of zones on the map. The first player to get
through all of these zones wins the game. You may choose to touch these zones
in any order. Above each zone, there is a cluster of splinter grenades that can
be shot, to cut off access to a zone. These can be used to through a wrench
into another player's path, forcing them to improvise to succeed.


## Scripts

### Player Manager

 > - Add the **[Player]** label to all players
 > - Reset the spawn order of all players to 0
 > - Reset the **Player-Count** to 0
 > - Set the **Player-Count** to the count of the number of **[Player]** labels

| #| `HEAR` **Initialize**||
| ---| ---| ---|
|| `LABEL` **+Players**| `ADD` **[Player]**|
|| `ORDER CHANGE` **+[Player]**| `SET` **0**|
|| `CHANGE` **Player-Count**| `SET` **0**|
|| `CHANGE` **Player-Count**| `SET` **+[Player] -> Count**|


### Player Serializer

 > - For every **Player** that exists that still has a `Spawn Order` of **0**,
 >   assign them a number from 1 to **Player-Count**

| #| `CHECK` **Player-Count > 0**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **1**|

| #| `CHECK` **This < Player-Count**||
| ---| ---| ---|
|| `ORDER CHANGE` **+[Player] +Order[0] +Random[1]**| `SET` **This**|
|| `CHANGE` **This**| `INCREMENT` **1**|

| #| `CHECK` **This - 1 === Player-Count**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **INFINITY**|


### Zone

 > - Whenever anything enters this zone
 >     - Ensure the object is a **[Player]**
 >     - If they are, then flip the switch on the equivalent `Spawn Order` **Zone Player Tracker**

### Zone Player Tracker

 > - When **This** is told to change
 >     - Give the respective `Spawn Order` **[Player]** a point
 >     - Remove the waypoint from **This** for that **[Player]**

### Win Checker

 > - Constantly check to see if a player has entered all of the zones and end
 >   the game if true

### Delay start

 > - Keep players from starting right away, give them the chance to plan out
 >   their path for X seconds before letting them run
