In order to create a properly isolated ecosystem of modules, we need to ensure
that everything for a aspect is built with certain considerations in mind. This
will ensure that we can easily have duplicates of a single aspect on different objects without worrying about interference.

 - If the aspect has events that recieve messages:
     - Global based messages should be safe to respond to
     - Group based message events should always have a `This.Parent`
       Conditional Filter applied to ensure that they aren't responding to
other gruops
 - Avoid changing any memory outside of Spawn Order, Local Object Variable, and
   Sending messages. The one exception is when using a global Power Channel designated as a messenging system using toggle. Modifying memory that anyone could rely on is dangerous and should be done with caution.
 - Double check for any potential debugging scripts. Look for score changes, sounds, nav points, coloring, etc.
 - Define the usage of each message response, the Spawn Order, and the purpose of the Local Object Variable
 - Ensure Spawn Order can be used for configuration
     - When configuring a number of 1+, ensure that the default of using a Spawn Order of 0 defaults to 1, or whatever the default should be
 - Keep in mind responding to Number Checks of the local object variable that you consider negative, 0, and positive numbers
 - If you are using local object variable checks then check for times when that variable needs to be reset to re-trigger changes
 - Ensure all script properties (Always Run, Condition Interrupt, Round Interrupt) are default to Off to avoid unwanted behaviour
 - Ensure the coloring on the objects match the coloring standards of the FDK
 - Where possible use labels for Configuration as well to effect scripts... this can lead to more extension possibilities, but keep in mind the universal label chart and how aspects are used across the board
 - Ensure your physics are set to Phased, unless otherwise necessary
 - Ensure the team is set to Neutral unless necessary
 - Create a test file that demonstrates the use of the aspect
 - Ensure a screenshot is taken for the aspect
