 - **Rotate Offset** - Something similar to Move Offset, where the rotation is
   based on the parent/target... or something like "look at"
 - **Channels for Object Scope** - Open up more memory options, allowing things
   like Objects tracking their own Value in tandem with ownership and state
etc. Lots of options (though probably a memory issue)
 - **Set the name of a NavPoint with a number** - With as many numbers as we
   have access to now, using NavPoints to visually display those numbers would
be SUPER helpful
 - **Add more conditions to multi** - Having things in Multi like
   Number:Checking could prove to be very very valuable moving forward
 - **Allow Filtering in Conditions** - Some conditions would be made much
   easier if we could do filtering to target specific players, or objects
 - **Save single objects as prefabs** - A lot of usefulness to prefabs is
   preset settings and scripts, with how complex objects can be it would be
great to be able to create prefabs out of single objects, especially with the
more modular scripting system
 - **UI Consistency** - Anywhere I can use a number, I'd like to be able to use
   any number (for example action target filtering can only take specific
numbers like number of this). And when I can use a conditional expression (like
a filter) I'd like to be able to use any conditional. For example, filters
being able to use action conditions (like number check) or conditions being
able to use filters instead of preset filters like Objects, Players, All
 - **Custom Gametype Label** - Currently we are limited to allowing only one
   mini-game on a single map effectively. It would be great if we can define
label's that match our gametype name so that way a map can suppurt multiple
custom gametypes. So a map could be built to support SpeedFlag, Halo Tactics,
Stockpile, Headhunter, without different variants.
 - **Filter for all objects that pass condition** - When doing something like
   Number Check, I want to be able to access the objects that passed the
condition. Currently we only have EXTRA. However, EXTRA is only for the
recently changed object. If this is a Global number that changed, then I don't
have access to the Object that met the condition. For example, Global Alpha is
changed to 5, a Number Check discovers that 5 equals this object's number. When
filtering, EXTRA returns the Global object, NOT the object that had a matching
number because that number didn't change, the global one did.
 - **Filter on the Spawn Action** - We currently have the ability to despawn
   another object using filters, but we cannot spawn other objects using
filters meaning that we can't abstract the act of spawning objects, they have
to manage their own spawning
 - **Use `This: Team` or `Activator: Team` in Conditions** - Right now we have
   to hardcode the team that we are working with into our script conditions. To
abstract this it would be great to be able to use the `activator` or `this`
team to keep those conditions generic and not have them be changed or setup for
every single team
 - **Control over what gets displayed in the combat log** - It is crucial for
   games to be able to update the combat log with significant events in the
same way that we can control waypoints, scoring, voice overs, etc. Perhaps
using a similar system to navpoints where we have a limit of verbs that we can
use.
 - **Use any Number data to set the Text on a NavPoint** - We have to do a lot
   of crazy work arounds and scripts to be able to properly set the waypoint to
our desired number. It would be great not to have to do this.
 - **Set Color on NavPoint based on Team Data** - Another thing that costs a
   lot of scripts are having to use different scripts for different colors,
that actually relate to a team. It would be much more valuable to be able to
set that color based on a team filter or something.
 - **Change Team action** - It would be extremely helpful for all gametype to
   be able to change the team of an object with an action. Then we can do
things like assign ownership for scoring for a Hill or capture strongholds and
label them for the team.
 - **Implicit values translation** - There are several different types of data
   that can be converted to other types. A Team, for example, could be the
equivalent of a Red Color or number of 1. Being able to use these values in
things like Number Check, Number Change, Spawn Order Change, NavPoint, Color
Change, etc. would enable a lot of flexibility.
 - **Player/Team/Object Serialization** - One of the most difficult things to
   do is to keep track of the exact player you are working on. If you setup a
player as a VIP, it would be nice to be able to store that Player's ID in a
Number channel, and then reference it in a Filter.
 - **[Action Filter] This:Labels ALL** - For configuration sake for re-usable
   prefabs it would be amazing helpful to have an action filter that would
handle things based on whether the object matched ALL of the labels, not just
one of the labels on the current object. This would allow us to create
combination based prefabs for when an object is both labeled as an Objective
AND an Zone for instance.
 - **Access Game Values using an Action Filter** - Currently we can only access
   a game value of an entity that is labeled as **THIS** or **ACTIVATOR**, and
it would be FAR more useful to be able to say pull out the spawn value of the
group parent.
 - **Use Spawn Order in conditions like Number Check** - Spawn order has proven
   to be a powerful tool for configuration, as such it would be extremely handy
to be able to use it in conditions.
 - **Two Variables for mathematic operators** - Currently the system takes two
   variables, the variable you are changing and the modifier. This creates an
equation of `A = A Operator B` or `A += B`. A lot of work is done to do `A = B
Operator C` or `A = B + C`, and it would would be extremely valuable to have
two source values that set the variable.
 - **Set default value for Object local variable** - Currently all objects have
   their local object scope variable default to 0 and it would be incredibly
useful for configuration sake to be able to set that value alongside Spawn
Order.
 - **Rename Spawn Order** - Honesly Spawn Order has grow in its usage from
   determining where players spawn, and instead determining anything that can
be represented by a number. Limits, Values, Order, ID, Grouping, etc.
 - **Ability to track the Boundary of other objects** - I'd like to be able to
   abstract essentially any event that could happen on another object. Boundary
in particular would be useful. In order for this to work properly we would need
to have action filtering in conditions, so we can say Boundary Check, This
object's Group Parent, Enter, Player (or any other action filter)
 - **Ability to set time based values with Number variables** - In terms of
   configuration, I would love to be able to access spawn order or local object
variables to be able to set the wait time or the round time, or the timer
delay/interval, etc.
 - **Player/Team scripts** - It would be incredibly useful to be able to have
   scripts automatically applied to each player or each team. For example, a
spawn script on a player that would automatically assign them a random number.
 - **Follow action** - Move offset is handy for a single movement, but a lot of
   the time we want to be able to follow and we have to manually do this
through heartbeats and moveoffset. It would be incredibly useful to just action
filter an object to follow, with a positional offset.
 - **More configuration settings per object available at the top level
   properties** - The Local object variable and spawn order are IMMENSELY
powerful for abstraction purposes. More variable locations on a per object
basis would allow more fine grained control over objects and would allow us to
avoid jumping hoops for certain situations.
 - **Script order/location/deleting/copying/pasting management** - Managing
   scripts is a hassle in the UI. The ability to re-order scripts, remove
things that aren't the last action/script, copying an entire script from one
object to another, etc. would be immensely useful. While in the menu, there are
a lot of buttons that aren't used, and utilizing them for things like delete,
or copy/paste, would be a god send.
 - **Nested Groups** - With the power of the new action filtering system and
   the Parent/Sibling relationship, having nested groups would prove extremely
powerful. Being able to access the siblings of one object, while another object
acts as the parent to other objects would allow for some very useful
abstractions
 - **Name Objects** - Please let us name objects for organization sake. These
   names don't have to show up in game outside of forge, but we definitely need
a way to keep track of objects.
