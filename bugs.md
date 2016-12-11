### #1

**Source:** Game Value
**Game Value:** Players: Team [Current]

Supposed to give you number of current players on the team, but instead gives
you 8... in both Forge and Customs.


### #2

Under the **Score: Changed** action, there is no access to the player scope,
you only have access to Global, Team, and Object.


### #3

The Player's Object Scoped Number, defaults to 0, however cannot be changed.

Recreate using a Terminal that increments the object scoped number on the
activator, then use **Score: Changed** to print the object scoped number on the
activator.
