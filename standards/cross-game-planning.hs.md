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
