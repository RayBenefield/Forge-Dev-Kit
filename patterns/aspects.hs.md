# Aspects

Aspects are a design pattern that I discovered that allows us to apply "aspects"
to objects, giving them specific functionality. This pattern allows us to take
a characteristic from a particular object and allow other objects to use it as
well. For example, if an object has a aspect of randomly exploding between 60
and 120 seconds, then that should be buildable as a aspect prefab that can be
used on any object.


## How they work

Aspects use a magical part of the Forge system that I've observed to be very
under-used. Within the Object Filtering system, there is a particular set of
filters that enable aspects. These filters revolve around the use of the Group
filters. Various filters exist like:

 - **Group Parents [add]**
 - **Group Parents [exclude]**
 - **Group Siblings [add]**
 - **Group Parents [exclude]**

Using these filters, but the act of simply grouping a aspect with an object, the aspect is able to identify its parent and then act on its parent. So anything you can do using object filters can be done using aspects.


## Examples

Let's go through building some simple aspects.

### Every Player Navpoint on Locate

Let's say that every time the **Locate** power channel is on, you want an
object to get a navpoint. To keep things simple, we'll just say there are no
other requirements so as soon as **Locate** power is on we will just add a
waypoint to the object. My aspect should look like this:

###### Script Brain

| #| `CHECK` **Locate -> On**||
| ---| ---| ---|
|| `NAV` **+Players**| `TARGET` **+This +Group.Parent -This**|

How do we use this? Easy, spawn any object you want to locate when the power is
on. Then group the object with this script brain. Make sure you do appropriate
techniques to make the object the parent of the group. Use a terminal to
tooggle the **Locate** channel and you will see the object get a Navpoint...
with NO scripts on it. This is an incredibly powerful technique and we can
demostrate that with some more wizardry.


### Every Player Toggle Navpoint on Locate

So similar to the last example, let's modify our aspect to also remove the
waypoint whenever the **Locate** channel is off.

###### Script Brain

| #| `CHECK` **Locate -> On**||
| ---| ---| ---|
|| `NAV` **+Players**| `TARGET` **+This +Group.Parent -This**|

| #| `CHECK` **Locate -> Off**||
| ---| ---| ---|
|| `NAV` **+Players**| `REMOVE` **+This +Group.Parent -This**|

Easy... same technique, anything grouped with this object as a sibling will get a navpoint. Try duplicating the aspect and adding them to several other objects.


### One Aspect to rule them all

Let's flip this on its head. Say I want LOADS of objects to get waypoints based on  the locate channel. Let's make a new aspect, or perhaps even modify the old one.

| #| `CHECK` **Locate -> On**||
| ---| ---| ---|
|| `NAV` **+Players**| `TARGET` **+This +Group.Siblings -This**|

| #| `CHECK` **Locate -> Off**||
| ---| ---| ---|
|| `NAV` **+Players**| `REMOVE` **+This +Group.Siblings -This**|

Folks, groups aren't just for forging anymore. ;) They make our lives easier as game designers. So now take this aspect, group it with TONS of objects, perhaps even up to the group limit. Make sure the aspect is the Group parent, and now every object will get its navpiont.


## Possibilities

This aspect concept can be used in multiple ways, groups is just one of them. For example, this can be done using the boundary filter as well. The unique thing with Groups is that you can guarantee a target by using Group Parent, applying behaviour to objects without using up a label just to track that one object. If used properly with Spawn Order, Labels, Team, Boundaries, etc. we can have extremely powerful and re-usable scripts that can be used easily by developers.
