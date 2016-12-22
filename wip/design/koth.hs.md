# King of the Hill

Teams fight for control of the active hill. You score `1` point for every
second your team controls the hill without being contested. The hill moves
every `X` seconds in a sequential order.

## Components

 - **Second Score Timer** - Sends a score event every `1` second
 - **Team Tagger** - Responds to **Tag** messages by setting the team for
   objects
 - **Standard Zone**
     - [**Held By Team**](../traits/held-by-team.hs.md) - Denotes the hill as
       being held by a specific team
     - [**Simple Scoring**](../traits/score-once.hs.md) - For every score
       event, add `1`
     - [**Contestable**](../traits/contestable.hs.md) - Multiple teams in the
       hill sets the hill to being **[Invalid]** and unable to score points
     - [**Order Spawning**](../traits/order-spawning.hs.md) - Multiple teams in the
       hill sets the hill to being **[Invalid]** and unable to score points
