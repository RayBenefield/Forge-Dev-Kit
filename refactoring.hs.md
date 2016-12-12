# Refactoring

## Why Do We Refactor in Forge?

In Halo's Forge we have several conditions in scripts that are hard to manually
trigger ourselves with a switch. These conditions are typically based on time:

 - Match Start
 - Round Start
 - Round Time X.XX
 - Score Changed
 - Player Spawn/Death
 - Boundary Check

Rather than tying logic explicitly to these events, we can "de-couple" our
logic by having these events trigger Messages, change Power, or changing
Numbers. Then we do things based on theose Messages, Power states, and Number
changes. This allows us to use switches to manually trigger our complicated
logic for testing/debugging purposes. For example:

| #1| `MATCH START`||
| ---| ---| ---|
|| `NAV` **+Players**| `TARGET` **[Objective]**|

The above script creates a waypoint/navpiont to any objects with the
**[Objective]** label. While developing, we can't manually test to make sure
that action actually works as we expect it to. Perhaps we want to know which
Objectives actually exist on the map? How do we **Refactor** this script to make it testable?

| #1| `MATCH START`|
| ---| ---|
|| `SEND` **Initialize**|

| #2| `HEAR` Initialize||
| ---| ---| ---|
|| `NAV` **+Players**| `TARGET` **[Objective]**|

By refactoring to a condition that is easy to control with a switch we are now
able to manually send the **Initialize** message from a terminal to make sure
that the NavPoints are being placed on the right objects.
