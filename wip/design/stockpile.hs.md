# Stockpile

Each team owns a stockpile zone. There are randomly spawning flags around the
map. Teams must grab flags and place them in their zone. Every `60` seconds,
any flags that are in the team's zone are scored for that team.

## Components

 - **Standard Flag**
     - [**Order Spawning**](../aspects/order-spawning.hs.md) - Spawns when
       ordered to
 - **Standard Zone**
     - [**Simple Label Scoring**](../aspects/score-once.hs.md) - Score 1 point
       for each Flag in your zone at score time
     - [**Owned By Team**](../aspects/owned-by-team.hs.md) - Denotes the zone as
       being owned by a specific team
     - [**Despawn Labels on Score**](../aspects/owned-by-team.hs.md) - Despawn
       all flags in the zone after scoring
