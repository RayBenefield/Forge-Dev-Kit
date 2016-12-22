# For Loop

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
