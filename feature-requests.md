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
