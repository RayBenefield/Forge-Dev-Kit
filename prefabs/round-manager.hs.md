# Round Manager

Manages all round tracking including a relative round based on spawn order. Set
the **Spawn Order** on this object to determine when the relative round cycles.
For example, if the **Spawn Order** is to 3, the **Current-Round** will be set
to 0 -> 1 -> 2 -> 0 -> 1... etc.


## Configuration

### Messages Memory

###### `INDIA` - Initialize

This is typically run on Match start. We use this to default all of the memory locations.

### Power Memory

###### `ROMEO` - Round-Active

If this is on then the Round is being played. If it is turned off, then the
Round has ended.


### Global \# Memory

###### `ROMEO` - Round-Number

Zero-indexed (like programming). Round 1 is 0, Round 2 is 1, Round 3 is 2, etc.

###### `CHARLIE` - Current-Round

Zero-indexed (like programming). Set as the Remainder of **Round-Number** and
the Spawn Order of the Round Manager (default to 7 thanks to Fury). This
results in numbers between `0` to `Spawn Order - 1`. This may be used to create
commonalities between a set number of rounds. For example, every first, second,
and third rounds work differently and then things cycle from there.

When **Round-Active** is `Off` then **Current-Round** is equal to the next round.

###### `VICTOR` - Volatile

This is a temporary memory location for Forge math.

### Spawn Order

###### `THIS`

The spawn order for this designates the number of differing rounds that you
have. For example if you have 3 different rounds this will be set to 3.


## Scripts

| #1 | `HEAR` Initialize| |
| ---| ---:| :---|
|| `CHANGE` **Round-Number**| `SET` 0|
|| `CHANGE` **Current-Round**| `SET` 0|

| #2 | `ROUND START`|
| ---| ---:|
|| `POWER` **Round-Active -> On**|

| #3 | `ROUND TIME` 0.00|
| ---| ---:|
|| `CHANGE` **Round-Active -> Off**|

| #4 | `POWER` Round-Active -> Off| |
| ---| ---:| :---|
|| `CHANGE` **Round-Number**| `INCREMENT`|
|| `CHANGE` **Volatile**| `SET` **Round**|
|| `CHANGE` **Volatile**| `REMAINDER` **Game Value -> `THIS` Spawn Order**|
|| `CHANGE` **Current Round**| `SET` **Volatile**|
