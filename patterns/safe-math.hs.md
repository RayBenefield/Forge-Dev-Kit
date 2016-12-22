# Safe Math

In Forge, mathematical operations, number setting, etc. modify the object in
place and doing so will trigger any events watching that channel. Say you want
to do `{Charlie} = {Delta} / {Echo}`. So you do `{Charlie} SET {Delta}` so you
can do `{Charlie} / {Echo}`, `Charlie` will change on the `SET` which can
trigger unwanted events that you have that watch for changes in `Charlie`.

In the FDK, to avoid this we use the local object variable as a middleman
variable. Because objects have a single responsibility in the FDK there is no
risk of things clashing. This allows you to set `Charlie` to `{Delta} / {Echo}`
without triggering anything watching `Charlie`.

```
Z = X {Operator} Y


e.g.:

Z = X / Y
Z = X * Y
Z = X % Y
```

| #1 | **{Some-Condition}**| |
| ---| ---:| :---|
|| `CHANGE` **This**| `SET` **{X}**|
|| `CHANGE` **This**| `{Operator}` **{Y}**|
|| `CHANGE` **{Z}**| `SET` **This**|
