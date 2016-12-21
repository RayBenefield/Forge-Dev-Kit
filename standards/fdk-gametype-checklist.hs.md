# FDK Gametype Checklist

The goal of the FDK is to create standardized gametype mechanics that provide
an easy means of building new gametypes. Naturally, gametypes that are added to
the FDK must meet some minimum requirements to be approved for the FDK.

## Considerations

 - Players Joining In Progress
 - Team existence
 - Navigation Waypoints
 - Sound Effects
 - Manually Trigger every event in the gametype using debugging tools
 - Request a Gametype Package Key
 - Define types of maps for the gametype
 - Player Scoring
 - Multiple Rounds
 - Spawn Order used for configuration
 - Memory isn't clogged by hardcoded values (avoid memory for each player, each
   team, each objective, etc.)
 - Color Standards are taken into account
 - File Descriptions
 - Map Setup instructions
 - Relevant files are set to public
 - Common patterns are followed (Game is started with the Game power channel,
   initialization happens with the Initialize message, etc.)
 - Scripting is reviewed to refactor into as many re-usable pieces as possible
 - Supports EVERY team
 - Proper use of FFA vs Team labels
 - Proper Timer Patterns are used
 - If being added to the FDK Core Package, it is added to every dev map
 - Test files are created
