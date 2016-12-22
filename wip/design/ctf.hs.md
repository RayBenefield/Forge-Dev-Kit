# Capture the Flag

Teams each have a flag. The goal is to grab the flags of the other teams and
capture them for yourself. First to `3` wins.

## Components

 - **Standard Flag**
     - [**Owned By Team**](../traits/owned-by-team.hs.md) - Denotes the flag as
       being owned by a specific team
     - [**Invalid when moved**](../traits/owned-by-team.hs.md) - If this moves
       then it is considered invalid
     - [**Resets after not held**](../traits/owned-by-team.hs.md) - Resets
       after `X` seconds of not being held
 - **Standard Zone**
     - [**Simple Label Enter Scoring**](../traits/score-once.hs.md) - Score 1
       point whenever an enemy Flag enters your zone
     - [**Owned By Team**](../traits/owned-by-team.hs.md) - Denotes the zone as
       being owned by a specific team
     - [**Despawn Labels on Score**](../traits/owned-by-team.hs.md) - Despawn
       flag after scoring
     - [**Invalid When Team Owned Label is
       Gone**](../traits/owned-by-team.hs.md) - If the team's flag is invalid
then this is invalid
