| #| `POWER` Round -> On|
| ---| ---|
|| `FORCE SPAWN`|
|| `DESPAWN` **+[Objective] +Activator.This**|

| #| `POWER` Round -> Off|
| ---| ---|
|| `DESPAWN`|

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `CHANGE` **+This.Boundary +Players -> Score**| `INCREMENT`|
|| `CHANGE` **+This.Boundary +Players +Team -> Score**| `INCREMENT`|
