# Gametype Packages

<sub>Courtesy of Ray Benefield</sub>

The ultimate goal of the Gametype Package system is to provide a set of up to
31 gametypes on a single map. Currently the Forge Engine allows you to include
objects or exclude objects on a per gametype basis. This is great, except for
now we have the potential to have TONS of mini-game gametypes to add to a
single map. In order to do that right now, we have to make copies of a map and
then build them for that new gametype as a variant. For example, a KoTH Plaza,
a StockPile Plaza, a Regicide Plaza, etc. Obviously this isn't suitable for
playing in custom games.

Ideally we want a single map that can support multiple mini-game gametypes and
when I select the Stockpile Gametype, the map just knows how to load the
objectives needed for it. And if I switch to King of the Hill, the map should
be smart enough to switch the objectives. As zones used in KoTH should not
exist in Stockpile and vice versa.


## Proposal

I believe we can achieve this using the special minigame labels that we have
now. In the mini-game settings you are able to turn these labels as include or not:

 - Mini-Game 1
 - Mini-Game 2
 - Mini-Game 3
 - Mini-Game 4
 - Mini-Game 5

I'm proposing that we use that on and off as a binary system. Every gametype is
assigned a binary combination as a key and all objects specifically for that
gametype are labeled with that binary combination of labels. This alone won't
work though as if we have a gametype keyed to `1`, `3`, `4`: we end up with
every gametype object that includes one of those three labels.

So to compensate for this we need an in-game mechanism that can recognize the
exact key and despawn all objects that don't match that key. This will require
single objects dedicated to each label. Each of these objects that exist will
turn on a power channel for that label (a label set to off in gametype settings
will not spawn its respective object). These power channels will be used to
calculate an ID number for the gametype (using a binary math system). Then
there will be 31 scripts (likely spread across 4 script brains) that will do a
number check and if it matches their assigned number, they will despawn
everything that does not pass their filter of label includes.

The biggest problem with this is the Timer pattern. For game timers to remain
reactive and responsive to manually triggered events, they will be despawned on
**Game -> Off**, have their timer have `Always Run` off, and then have an
`Always Run` on **Game -> On** `Force Spawn`. This means that if despawning is
the only way to turn off objects then a Stronghold Score Timer and a Stockpile
Score Timer will both ignore being turned off at the beginning.

<sub>Courtesy of the help from Carson Barry (CaptainPunch)</sub>

This could be gotten around by re-running the gametype key filter again either
on heartbeat or after **Game -> On**, perhaps with a little of a wait. This
ensures that when the game is turned on any things that only spawn once for
that gametype are turned off. A heartbeat would be needed for things that would
use `Always Run` spawning throughout the match. Perhaps like Stockpile flags.
If this becomes a bigger problem, then the normal game heartbeat should be
standardized to .1 seconds, while the gametype filter heartbeat is set to .05
seconds.


## Caveats

There are some problems with this system:

 - Having a potential heartbeat that runs on every single gametype just to keep
   objects filtered could create problems
 - Objects are limited to only 4 labels, so this would restrict what kind of
   key they can get
     - If a gametype requires 2 labels on a single object, they can only get a
       key with 2 numbers or less
 - This prevents the ability to support variants for a gametype in the core
   package as the labels are now used for gametype selection rather than
variant selection
 - In general this may require more work than it is worth

 > Not actually a problem, traits are set on a per gametype basis, so this is not a problem
 - ~~This is limited also by only 4 traits, so gametypes that use drastically
   different traits may not be able to be included in the core package~~
     - ~~This could be the major limitation as gametypes might not agree on how
       to handle a ball carrier~~
     - ~~Something standard like Flag Carrier traits for slowing down will work
       best~~
     - ~~It is not possible to stack traits on top of each other, a player can
       only have one trait at a time~~
     - ~~Base Player traits essentially MUST remain the same across all
       gametypes, so a true core package needs to keep standard Halo traits~~


## Gametype Key Combinations

 1. None
 1. 1
 1. 2
 1. 3
 1. 4
 1. 5
 1. 12
 1. 13
 1. 14
 1. 15
 1. 23
 1. 24
 1. 25
 1. 34
 1. 35
 1. 45
 1. 123
 1. 124
 1. 125
 1. 134
 1. 135
 1. 145
 1. 234
 1. 235
 1. 245
 1. 345
 1. 1234
 1. 1235
 1. 1245
 1. 1345
 1. 2345
