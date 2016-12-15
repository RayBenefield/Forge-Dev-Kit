# Equality

The goal of equality is to have the minimum kills on all other players. For
example, with 4 players in the game, you get a point for killing all three
other players. The catch is that you can't kill a player you have already
killed unless you have already killed all other players. Killing a player
again, before killing all other players, will result in you losing all
progress. You must essentially ensure that you treat all players equally and
show no favoritism.


## Mechanics

 - Players you have already killed will be flagged as already killed by you,
   and will receive a waypoint on their head periodically (perhaps every 15
secondsor all the time) to indicate that you should not kill this player.
 - When all players have been killed once (they have all been flagged), then
   the flags will clear and you will score a point
 - If you kill a player that is flagged as already killed, then all progress
   will be lost... if you don't have any other progress and that was the only
player flagged, you will lose a point
 - The game will play for X minutes and the player with the highest score at
   the end wins.


## Side Effects

 - A player that doesn't get killed often will end up being teamed up on, as
   players will end up as only having that player left to kill
     - The above can result in temporary team ups
     - Player A and Player B have already killed each other and would suffer
       from killing each other, Player C has not been killed by either, so
Player A and B team up to take down player C... the first to kill Player C will
end up getting the point
 - As soon as one of the players teaming up gets the point, everyone else
   becomes free game for them, and the other player(s) need to run away (and
can't kill them because it would make them lose a point or progress).
     - Player A and B find Player C, Player A gets the kill and hence the point
     - As soon as Player A gets the kill, killing Player B becomes fair game
       for Player A
     - Player B must now get away without killing player A, while A chases for
       the kill
 - The periodic waypoint will ensure that players have to keep track of which
   players are marked and who they are, if they don't they have to wait for the
waypoint to avoid loss of progress or a point
     - This gets a little more complicated when you consider seeing navpoints
       through walls and multiple players in one area
 - Players can lie to other players about not needing to kill them, because no
   player knows the progress of another player, they won't know whether or not
the player is lying and waiting to take advantage of the team up
     - Player A sees that Player B is not killing them, so they propose a team
       up to Player B
     - What Player A doesn't know is that Player B hasn't killed player A yet
     - While hunting for Player C, Player B takes advantage of the situation
       and kills Player A
