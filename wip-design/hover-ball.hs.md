# Hoverball

 > - **Objective 1** - Balls
 >     - **Ownership**: Neutral
 >     - **Location**: Carried
 > - **Objective 2** - Zones
 >     - **Ownership**: Neutral
 >     - **Location**: Static
 > - **Score Frequency** - 1 second
 > - **Hold To Score Duration** - Not Required

In Hoverball there are multiple neutral balls around the map, along with
multiple floating neutral zones around the map. When a ball is thrown into a
zone, it hovers in the center of it and starts scoring points for the team of
the player who put it in the zone. If another ball is thrown into the goal, the
other ball is dropped out of it, and replaced with the new ball.


## Score Manager

| #| `HEAR` **Score-Team**|
| ---| ---|
|| `CHANGE` **Player.Score**| `INCREMENT` **Activator.Order + 1**|
|| `SCORE` **Player +Activator**| `INCREMENT` **Activator.Order + 1**|

## Zone

| #| `OBJECT ENTERS`||
| ---| ---| ---|
|| `PHYSICS CHANGE` **+This.Boundary +This.Order==Number -> Normal**|
|| `CHANGE` **+This.Boundary +This.Order==Number**| `SET` **0**|
|| `CHANGE` **+Activator**| `SET` **This.Order**|
|| `PHYSICS CHANGE` **+Activator -> Phased**|

| #| `OBJECT EXITS`||
| ---| ---| ---|
|| `PHYSICS CHANGE` **+Activator -> Normal**|
|| `CHANGE` **+Activator**| `SET` **0**|
|| `CHANGE` **+Activator**| `SET` **This.Order**|
|| `PHYSICS CHANGE` **+Activator -> Phased**|

## Ball

| #| `CHECK` **This > 0**|
| ---| ---|
|| `FOLLOW` **+This -> +[Container].Order==This**|

| #| `HEAR` **Score**|
| ---| ---|
|| `SEND` **Score-Team**| `TRANSFER` **This**|
