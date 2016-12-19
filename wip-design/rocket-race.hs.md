| #| `PLAYERS ENTER`||
| ---| ---| ---|
|| `SEND` **Score**| `TRANSFER` **Activator**|
|| `DESPAWN`|

| #| `HEAR` **Objective**| `ALWAYS RUN`|
| ---| ---| ---|
|| `FORCE SPAWN`|
|| `DESPAWN` **+[Objective] -This.Order==Activator**|

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `SCORE` **Activator.Team**| `INCREMENT`|

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **This.Order** `RANDOM`|
|| `SEND` **Objective**| `TRANSFER` **This**|
