# Patterns

Patterns refer to a particular way to solve a problem. These patterns can help
you solve extremely complex problems in Halo Forge's scripting system.


## For Loop

Sometimes you have to repeat something many many times. Perhaps you are
scrolling through a list of players from a filter, or you have to play a sound
`{LIMIT}` times. Using the Object Scoped Number `This` variable on an object as an
iterator we can go from `{Start}` to `{Limit}`. You can also use the Object
Scoped Number `This` in a filter to run through a series of players.

```js
for (var i = {Start};  i < {Limit}; i++) {
    {Do-Something-Here}
}


e.g.:

for (var i = 0;  i < numberOfPlayers; i++) {
    Player[i].applyTrait(alpha);
}
```

| #1| **{Some-Condition}**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **{Start}**|

| #2| `CHECK` **This** < **{Limit}**||
| ---| ---| ---|
|| **{Do-Something-Here}**
|| `CHANGE` **This**| `INCREMENT`|


## Safe Math

In Forge, mathematical operations, number setting, etc. modify the object in
place and doing so will trigger any events watching that channel. Say you want
to do `{Charlie} = {Delta} / {Echo}`. So you do `{Charlie} SET {Delta}` so you
can do `{Charlie} / {Echo}`, `Charlie` will change on the `SET` which can
trigger unwanted events that you have that watch for changes in `Charlie`.

In the FDK, to avoid this we use a middleman variable `Volatile`.  Gametypes
and Prefabs in the FDK should not be watching `Volatile` as it is expected to
be flimsy and ever changing.  `Volatile` is a temporary variable. This allows
you to set `Charlie` to `{Delta} / {Echo}` without triggering anything watching
`Charlie`.

```
Z = X {Operator} Y


e.g.:

Z = X / Y
Z = X * Y
Z = X % Y
```

| #1 | **{Some-Condition}**| |
| ---| ---:| :---|
|| `CHANGE` **Volatile**| `SET` **{X}**|
|| `CHANGE` **Volatile**| `{Operator}` **{Y}**|
|| `CHANGE` **{Z}**| `SET` **Volatile**|
