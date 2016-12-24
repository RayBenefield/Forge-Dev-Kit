# Group Messaging

Some message channels are more useful when they are used on a group to group
basis. This is not native functionality for Forge, but we do have a way to
accomplish this.


## Message from This.Parent

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

**NOTE**: If the object has NO parent (not in a group), this will still trigger
as if it received a message from its parent, as such it will be effected by ALL
messages of this type.

**NOTE**: The parent must be sending itself as the activator for group
messaging to properly recognize messages from the parent. Otherwise it will add
its parent and not filter out its parent as the activator.

**TODO**: Analyze the effects of the message activator being the actual
activator (of like a boundary check). This could allow boundary checks to
trigger parent based messages on the objects entering the boundary of the
message sender (so a flag entering a zone can have the zone, send a message to
the flags children as if the flag had sent it).

## Message from This.Sibling

The reverse can be checked as well, like a child telling a parent to Spawn
itself (since objects can only spawn themselves, not be spawned with an action
filter.

**TODO**: This needs to be verified by checking if siblings include the parent

| #1 | **Spawn-Message**| |
| ---| ---:| :---|
|| `CHANGE` **This**| `SET` **-1**|
|| `CHANGE` **This**| `MULTIPLY` **+This +Activator -Group.Siblings -This -> Count - 1**|
> Do things based on 0 if false and 1 if true
