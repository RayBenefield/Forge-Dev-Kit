 - **Game Manager**
     - Game-Active - On/Off
 - **Round Manager**
     - Round-Active - On/Off
     - Round-Number - 0+
     - Current-Round - 0+
     - Spawn-Order -  Unique-Rounds
 - **Round Player Spawner**
     - Player Spawn-Order - 1+
 - **Round Objective Spawner**
     - Objective Spawn-Order - 0+
 - **Player Valuer**
     - Player-Score
 - **Team Valuer**
     - Team-Score
 - **Player Scorer**
     - Score - Player
 - **Team Scorer**
     - Score - Team

```
// Fury Event Sequence

Match-Start
|- Initialize
|- |- Round-Number = 0
|- |- Current-Round = 0
|- |- |- Player-Spawn-Order = Current-Round
Round Start
|- Round-Active On
Round-Time 0.0
|- Round-Active Off
|- |- Round-Number += 1
|- |- Current-Round = Round-Number % Unique-Rounds
|- |- |- Player-Spawn-Order = Current-Round
```

## Objective 1 -> Objective 2 (Container) Gametypes

### Event Sequence

```
Match-Start
|- Initialize
|- |- Game-Active Off
|- |- |- Despawn Objectives
|- |- |- Despawn Timers
Round Start
|- Game-Active On
|- |- Spawn Objectives
|- |- Spawn Timers
|- |- |- On Score Timer
|- |- |- |- In Objectives Boundary
|- |- |- |- |- Player Score
|- |- |- |- |- |- Team Score
Round-Time 0.0
|- Game-Active Off
|- |- Despawn Objectives
```

#### Assault

 > - **Objective 1** - Balls
 >     - **Ownership**: Neutral
 >     - **Location**: Carried
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Static
 > - **Hold To Score Duration** - 5 seconds
 > - **Score Frequency** - Immediate

#### Battle Golf

 > - **Objective 1** - Balls
 >     - **Ownership**: Team
 >     - **Location**: Physics
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Static
 > - **Hold To Score Duration** - Not Required
 > - **Score Frequency** - Immediate

#### Oddball

 > - **Objective 1** - Players
 >     - **Ownership**: Team
 >     - **Location**: Movement
 > - **Objective 2** - Balls
 >     - **Ownership**: Neutral
 >     - **Location**: Static
 > - **Hold To Score Duration** - Not Required
 > - **Score Frequency** - 1 second

#### Parkour

 > - **Objective 1** - Players
 >     - **Ownership**: Neutral
 >     - **Location**: Movement
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Random
 > - **Score Frequency** - Immediate
 > - **Hold To Score Duration** - Not Required

#### King of the Hill

 > - **Objective 1** - Players
 >     - **Ownership**: Team
 >     - **Location**: Movement
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Sequential
 > - **Score Frequency** - 1 second
 > - **Hold To Score Duration** - Not Required

#### Warpath

 > - **Objective 1** - Players
 >     - **Ownership**: Team
 >     - **Location**: Movement
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Static Path
 > - **Score Frequency** - 1 second
 > - **Hold To Score Duration** - Not Required

#### Extraction

 > - **Objective 1** - Players
 >     - **Ownership**: Team
 >     - **Location**: Movement
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Sequential
 > - **Hold To Score Duration** - 5 seconds
 > - **Score Frequency** - Immediate


#### Stockpile

 > - **Objective 1** - Flags
 >     - **Ownership**: Neutral
 >     - **Location**: Carried
 > - **Objective 2** - Team Based Zones
 >     - **Ownership**: Team
 >     - **Location**: Static
 > - **Score Frequency** - 60 second
 > - **Hold To Score Duration** - Not Required

#### Capture the Flag

 > - **Objective 1** - Flags
 >     - **Ownership**: Team
 >     - **Location**: Carried
 > - **Objective 2** - Zones
 >     - **Ownership**: Team
 >     - **Location**: Static
 > - **Score Frequency** - Immediate
 > - **Hold To Score Duration** - Not Required

#### Ricochet

 > - **Objective 1** - Balls
 >     - **Ownership**: Neutral
 >     - **Location**: Carried
 > - **Objective 2** - Zones
 >     - **Ownership**: Team
 >     - **Location**: Static
 > - **Score Frequency** - Immediate
 > - **Hold To Score Duration** - Not Required

#### Race

 > - **Objective 1** - Vehicles
 >     - **Ownership**: Team
 >     - **Location**: Carried
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Sequential
 > - **Score Frequency** - Immediate
 > - **Hold To Score Duration** - Not Required

#### Rocket Race

 > - **Objective 1** - Vehicles
 >     - **Ownership**: Team
 >     - **Location**: Carried
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Random
 > - **Score Frequency** - Immediate
 > - **Hold To Score Duration** - Not Required

#### Headhunter

 > - **Objective 1** - Skulls
 >     - **Ownership**: Team
 >     - **Location**: Carried
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Random
 > - **Score Frequency** - Immediate
 > - **Hold To Score Duration** - Not Required


### Conventions

 - The **Local Variable** or the **Spawn Order** on an objective
     - [default: **Local Variable**] Is the dynamic team that it belongs to
       (static team is tied into the object's team value)
     - [default: **Spawn Order**] Is the value it is worth when scoring
     - The order number it spawns in a sequence
     - How many of its partner objective is required to score
 - **Spawn Order** is used for number configuration for anything that isn't a
   spawn point or player

### Components

#### Team Tagger

The objective sends a **Tag/Team** message and the Team. Tagger responds by
setting the sender's number as the respective team.

 - **Team** - 1 for each team
 - **Spawn Order** - Number for team (1 Red, 2 Blue, etc.)
 - **Color** - User <Team-Number> (User 1, User 2, User 3, etc.)

`Team Tagger`

| #| `HEAR` **Tag-Team**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **This.Order**|
|| `CHANGE` **This**| `MULTIPLY` **<li>+Activator.Boundary <li>+This.Team <li>-Dead <li>+First -> Count**|
|| `ORDER CHANGE` **+Activator +Group.Siblings -Activator +[Team-Based]**| `SET` **This**|

`Object calling the tagger`

| #| `PLAYERS ENTERS/EXITS/IN`||
| ---| ---| ---|
|| `SEND` **Tag-Team**|


#### Handling Team Scoring

I need to look at handling scoring more abstractly based on FFA vs Teams. I can
probably use the [team_include] and [ffa_include] labels.

`Team Scoring Trait`

 - **Labels** - [Team-Based], [Scoring]

| #| `CHECK` **This > 0**||
| ---| ---| ---|
|| `CHANGE` **+[Scorer] +Order==This.Order**| `SET` **This**|
|| `CHANGE` **This**| `SET` **0**|

`Valued Object that wants Team Scoring`

 - **Spawn Order** - The amount of points this should score

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **This.Order**|
|| `CHANGE` **This**| `MULTIPLY` **+This +[Scoring] -> Count**|
|| `CHANGE` **+This +Group.Siblings +[Scoring]**| `SET` **This**|
|| `CHANGE` **This**| `SET` **0**|


#### Objective Valuer

On an event the valuer scrolls through any object with its two objective type
labels on it and then sets the scorer's number to the value. For example, for
Oddball on the 1 second timer, grab all of the objects with a Label of Ball and
Player, for each object change the Number of the Team Scorer to the Spawn Order
of the object.


#### Team Scorer

When the team scorer's number is set it adds the number to this team's score
and then reset to 0.

##### Options

 - Objectives with two labels send score message so their spawn order can be
   used for value
 - Get count of everything with the two labels, loop through them to trigger a
   score based on spawn order (marking as scored), then clearing the scored
marker
 - Change the score channels, to trigger a change that displays updated score
 - Use object local variables on scorer to add value
