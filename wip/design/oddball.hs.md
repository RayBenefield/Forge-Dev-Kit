# Oddball

Teams fight for control of the ball. You score `1` point for every second you
hold the ball.

## Components

 - **Second Score Timer** - Sends a score event every `1` second
 - **Team Tagger** - Responds to **Tag** messages by setting the team for objects
 - **Standard Ball**
     - [**Held By Team**](../aspects/held-by-team.hs.md) - Denotes the ball as
       being held by a specific team
     - [**Simple Scoring**](../aspects/score-once.hs.md) - For every score
       event, add `1`
     - [**Resets after not held**](../aspects/owned-by-team.hs.md) - Resets
       after `X` seconds of not being held
