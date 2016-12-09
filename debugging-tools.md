## What is Debugging

From Wikipedia:

> Debugging is the process of finding and resolving of defects
that prevent correct operation of computer software or a system.

Why debug in Halo? Because not only can there be bugs in the engine, your
logic, or you want to make sure that your content is working consistently, but
it also speeds up your development time. Rather than taking guesses at whether
or not something will work, good debugging tools will lead to things that you
can guarantee works.

The goal of debugging is great software. The key to great debugging is
information. There are various ways to provide information during development
thanks to the Monitor's Bounty update for Halo. These new ways to acquire
information are key to providing solid debugging tools that help you build the
best software possible.


## Sources of Information

The best sources of information are ones that don't require you opening the
menus in Forge. Most of these sources are possible thanks to the new
`Forge:Include` label. If you have more ideas for sources of information,
please submit an issue so we can discuss adding it to this material.


 - **Score: Change**

This action is extremely powerful for debugging numbers, which are a huge
source of information in the forge scripting engine. There are several memory
categories, functions, and systems dedicated specifically to numbers. Global,
Team, Player channels, Object scope, Spawn Order, Counting, Number Checking,
Score, Randomization, etc. Tons of systems work with numbers so having a way to
debug those numbers is crucial.

 - **NavPoints**

NavPoints are not just for playing Halo. They can be a valuable source of
information in Forge. NavPoints are viewable from large distances (up to 500
units) and have many visual settings including viewing distance, color, and
text. Mixing all of these together can lead to amazing information that can be
seen at a glance, tell stories, and even be localized to a specific area of the
map.

 - **Decals**

Decals have proven to be a very powerful tool for forgers, and with the
Monitor's Bounty update, they just got more powerful. Especially for numbering
things. Use Move: Offset to tie them to particular entities on level. Because
of their piecemeal nature they can be very versatile, especially for
identification.

 - **Effects and Lights**

Sometimes you don't need characters, sometimes just color and attention
grabbing is all you need in that case take advantage of effects and lights. Use
their various colors, their very eye grabbing characterictics to really bring
attention to an area. Perhaps you use them to color entire rooms for easy
visual organization during development. Lens Flare is particularly useful on
lights.

 - **Custom Objects**

Even building special objects for debugging can work well. But you may not want
to overdo it you could end up spending mor etime building tools than actually
building and spend too much budget on them.
