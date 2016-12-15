# Halo Forge Development Kit [Halo FDK]

Welcome to the Halo FDK. With the release of the Monitor's Bounty update,
Forge's scripting system has become more like a scripting language. There are a
lot of aspects of it that allow Forgers to generalize, re-use, and standardize
their scripting systems for gametypes. Software engineering practices like
refactoring, decoupling, modularity, debugging, testing, etc. have become more
important than ever.


## Table of Contents

 - [Overview of Goals](#overview-of-goals)
 - [Inspiration](#inspiration)
 - [Design Documents](#design-documents)
 - [Prefabs](#prefabs)
 - [Standards](#standards)
 - [Documentation](#documentation)
 - [Collaborators](#collaborators)

## Overview of Goals

The FDK hopes to achieve a lot by bringing together the community in an open
source fashion:

 - Push a collaborative open source effort between forgers to improve the Halo
   Community (e.g. community decisions, issues, pull requests, version
tracking, etc.)
 - Bringing back classic Halo gametypes for the community to enjoy (e.g.
   Stockpile, Headhunter, VIP, Juggernaut, Regicide, etc.)
 - Enabling multiple gametypes based on the new Mini-Game gametype on a single
   map (e.g. Adding all of the above and more to the same map without multiple
map variants)
 - Provide a location to find scripting documentation in a readable accessible
   form (e.g. documenting the memory system, documents in Markdown format,
etc.)
 - Expose design documents for all gametypes that are added to the FDK to serve
   as an example for other forgers (e.g. How to build KoTH, Race, Invasion,
Fury, etc.)
 - Pushing gametypes to the limits in terms of customization for forgers (e.g.
   Infinite phases in Invasion, Unlimited hills for KoTH, etc.)
 - Setting up centralized standards like similar channel usage (e.g. Message
   Channel India for Initialization, Power Channel Golf for Game On/Off, etc.)
 - Provide patterns to common problems in complex scripting (e.g. Tracking
   Player Deaths, Looping over an arbitrary number of objects, etc.)
 - Encourage reusable prefabs to make creating complex gametypes easier and
   faster (e.g. Game Managers, Round Managers, Spawn Managers, etc.)
 - Put a focus on debugging and testing to ensure faster iteration, higher
   quality, and stability (e.g. Verify gametypes work in Forge using switches,
navpoints, score, etc.)
 - Provide a centralized place to file bugs and feature requests for the
   scripting system (e.g. Maximizing the action filtering system, fixing memory
channels, etc.)
 - Provide reason for 343 to continue supporting and improving the User
   Generated Content capabilities of Halo (e.g. more Forge support, more
Gametype options, etc.)


## Inspiration

> A good friend of mine, and fellow team member on Creative Force, Carson Barry
> (Captain Punch), proposed a project internally for Creative Force. That
> project was called **Latchkey**, which was to comprise of a bunch of
> components that could be used together to construct complex gametypes. If you
> have ever played Halo: Reach Invasion, it was like that on steroids. The goal
> was to introduce new mechanics, objectives, etc. to allow the creation of
> whatever you wanted.

> With that being worked on right now with Invasion as the first end product,
> using a bunch of objectives and mechanics, I decided that it would probably be
> really good if there were standards that would make this an even easier
> endeavor. With the new scripting system, there was a lot of potential for
> things to go wrong and not work together, but there was also a lot of potential
> for things to go very right and actually make a project like this easier.

> So a huge thank you to Carson for leading the way and paving the path of what
> will be a huge community initiative to stay in sync with each other and make
> gametype development in Halo Forge that much easier.

> **- Ray Benefield**



## Design Documents

These are design docunents for FDK approved gametypes:

 - [Fury](design-docs/fury.hs.md)


## Prefabs

These are the FDK tools to assist in creating gametypes:

 - [Game Manager](prefabs/game-manager.hs.md)
 - [Round Manager](prefabs/round-manager.hs.md)
 - [Round Spawner](prefabs/round-spawner.hs.md)


## Standards

These are the documents that define what the standards of the FDK are:

 - [Script Template](standards/haloscript-template.hs.md)
 - [Universal Memory Chart](standards/universal-memory-chart.hs.md)
 - [Gametype Checklist](standards/gametype-checklist.hs.md)


## Documentation

These are reference documents describing the mechanics of Halo Forge and its
scripting system:

 - [Memory](docs/memory.hs.md)
 - [Debugging](docs/debugging.hs.md)
 - [Patterns](docs/patterns.hs.md)
 - [Refactoring](docs/refactoring.hs.md)


## Collaborators

|[![Ray Benefield](http://gravatar.com/avatar/e931b13306ea1022549766266727f789?s=144)](https://github.com/RayBenefield) |
|:---:|
| [Ray Benefield](https://github.com/RayBenefield) |
| [XBL GT: `Ray Benefield`](https://account.xbox.com/en-US/Profile?GamerTag=Ray%20Benefield) |
| Creative Force Founder |
| Community Cartographer |
| [Solution Architect](https://en.wikipedia.org/wiki/Solution_architect) |
