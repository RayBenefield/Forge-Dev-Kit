# MMO

A Halo MMO is created with tons of cooperative maps that have completable
objectives... these maps are the equivalent of quests, raids, instances, etc. I
think we can create an MMO type experience if we track games and generate
conclusions across a wide set of games, rather than think on a single game to
game level. We do this by tapping into the Halo API. Players that are playing
the MMO, are registered to a particular site. When a "quest" is completed by
the player, this is recorded by the site and progress is tracked across all of
these games. This overarching tracking allows us to control progress. For
example, a player may not be counted for completing a particular quest until
they have completed the pre-requisite quest.


## Quests

These quests are cooperative maps that require X number of players to complete.
Perhaps an instance/dungeon can only be run with a max of 4 players. Perhaps a
solo quest can only be played by just you. And perhaps a raid quest must be
completed with 16 players. This opens up a WORLD of possibilities. We just have
to make quests fun at this point. I think inspiration from Destiny can prove to
be very useful. Destiny is a mostly instance based MMO, with a max of 16
players per instance. Why can't we then create the experience through Halo and
its API?


## Level, Experience, and Gear

How do we control progression and persistence? We keep track of what quests a
player has completed and how and we use that to track experience gained based
on stats of previously completec quests. If a player or a party has X amount of
experience combined, they are authorized to use a different higher level
gametype. This different gametype gives them access to different weapons on
spawn and throughout the level. The lower level you are the worse weapons your
gametype gives you. Theoretically we can have 30 experience levels as we can
create up to 30 different combination of labels on a single object. This means
we can spawn or despawn for various levels.


## Variety

There are a LOT of things we can do to provide variety:

 - We can provide experiences based on "squads" going into a map. Every player
   chooses to be part of a different squad before running the game. Perhaps you
require all players to be on the same squad.
 - Different weapons on different quests. Perhaps being level 10 on one quest
   vs level 10 on another quest gives you access to different weapons.
 - Perhaps some quests have a cap to the amount of experience you can gain, or
   perhaps experience is calculated differently based on the quest. Perhaps
objects with a label of **[Boss]** gives that object a TON of experience and
makes them way more valuable.
 - Since different experience levels are different gametypes that can provide
   different player traits. We can give different starting health, different
starting weapons, different grenades, different spartan abilities and power,
etc.


## Building a Player Base

With the many Forgers in the community we can create TONS of quests for the MMO
and have user generated content by nature of people just building new maps in
Forge. With all of this content we can do lots of things.

 - Provide SOOO much challenge that it requires people to party up with each
   other just to ease difficulty
 - Have people build guides to maps for strategies, perhaps youtube videos to
   optimize your ability to take on the game
 - Open up an API to a player's statistics so websites like Forgehub and Reddit
   can share the player's stats
 - Have "events" where certain quests give more experience or becomes available
   during these events.


## Building a Developer base

We need people to build content for this game. We can encourage them by:

 - Provide prefabs for standard objectives
 - Design some simple AI systems to implement into maps
 - Provide a submission system so people can submit quests with X criteria
 - Offer recognition for being one of the quest creators for a huge initiative
 - Design all of the game rules up front and documented (like the base player
   traits for each level)


## Speeding up release

 - Since long term progression is possible we don't need content for all 30
   levels early on
 - Use an established system that currently exists, perhaps DND for experience
   level progression and a model for experience gain
