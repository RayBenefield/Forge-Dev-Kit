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


## Conditional Math

There are several ways that we can use math to essentially serve as conditionals. Because multiplying by 1 results in the same value and inversely multiplying by 0 results in a 0, we can essentially do the equivalent of:

```
// If condition is false
if(result > 0) {
    // Do Stuff
} else if (result === 0) {
    // Ignore me
} else if (result < 0) {
    // Do negative things (probably with the absolute value of this)
}
```

This is extremely powerful giving us the ability to replicate having nested
conditional logic as you can respond to any event and say "if this is true, AND
we've got stuff then do this".

### Boolean Conditional - At least one object exists

This becomes more useful when you consider that we have access to counting
objects with filters. So we can say "if you send me this message and this thing
exists, then do this.' This is what it looks like:

| #1 | **{Some-Condition}**| |
| ---| ---:| :---|
|| `CHANGE` **This**| `SET` **{Default-Value}**|
|| `CHANGE` **This**| `MULTIPLY` **+Activator.Boundary +First -> Count**|
>  Do something based on **This** being 1 or 0, more validation or
transformation is a good thing to try here

### Revesrse Boolean Conditional - No objects exist

Sometimes your filters will have to result in seeing if the list is empty. If
you do this you come up with 0 and 1, but 1 is bad in this case. To get around
this we start with a negative number instead, then substract 1 from the count
to create a 0 and -1 result and then multiplying -1 by the negative default
value will result in a positive value if the list filter has nothing in it.

| #1 | **{Some-Condition}**| |
| ---| ---:| :---|
|| `CHANGE` **This**| `SET` **{Default-Value}**|
|| `CHANGE` **This**| `MULTIPLY` **-1**|
|| `CHANGE` **This**| `MULTIPLY` **+Activator.Boundary +First -> Count - 1**|
>  Do something based on **This** being 1 or 0, more validation or
transformation is a good thing to try here

## Group Based Messaging

Some message channels are more useful when they are used on a group to group
basis. This is not native functionality for Forge, but we do have a way to
accomplish this.

### Message from This.Parent

Sometimes the parent has to tell its children to go do something. The Parent
will send a message like "Someone entered my Boundary." and the children will
respond to that. This is how you do that.

| #1 | **Boundary-Message**| |
| ---| ---:| :---|
|| `CHANGE` **This**| `SET` **-1**|
|| `CHANGE` **This**| `MULTIPLY` **+This +Group.Parent -This -Activator -> Count - 1**|
> Do things based on 0 if false and 1 if true

Using [Reverse Boolean Conditional Math](#reverse-validation-math) we can
determine if the message was sent by our direct parent. We check for if the
sender is our parent by adding our parent and then trying to remove the
activator. If removing the activator results in no objects left then that was
our parent, otherwise the activator was not our parent so we want to return 0
to invalidate future calculations.

### Message from This.Sibling

The reverse can be checked as well, like a child telling a parent to Spawn
itself (since objects can only spawn themselves, not be spawned with an action
filter.

**TODO**: This needs to verify by checking if siblings includes the parent

| #1 | **Spawn-Message**| |
| ---| ---:| :---|
|| `CHANGE` **This**| `SET` **-1**|
|| `CHANGE` **This**| `MULTIPLY` **+This +Activator -Group.Siblings -This -> Count - 1**|
> Do things based on 0 if false and 1 if true
