# Memory System

<sub>Courtesy of Yumudas Beegbut and Ray Benefield</sub>

Halo 5's Forge runs off a Memory system where values are stored and used in
scripts. There are many options to store and manipulate data so this document
sheds some light on the system.


## Types of Data

### Message

**Messages** serve as Event notifications. They happen once and are discarded.
These are good to use when what you are looking at is an event that happens
every once in a while and there is no obvious start or end. Anything Message
can do can be replicated by **Power State**, **Number**, and **Score**.

### Power State

**Power** State is represented by `On` or `Off`. These are the equivalent of
booleans in programming. These are valuable for keeping the state of an event.
If you are working with data that can logically have a start or end, and be on
or off, or active vs inactive, then a **Power** State may be your best location
for that data. Every change of a **Power** state also serves a similar purpose
to a **Message**.

### Numbers

**Numbers** can be set from `-10,000` to `10,000` using constants (perhaps
higher using math). They are the most abundant memory slots so understanding
what your options with them are will give you a lot of control over the system.
In a pinch Number data can serve the same purpose as a **Power** channel. For
example, `Negative` (Off) vs `Positive` (On) numbers, or `0` (Off) vs `1` (On).
They can also serve the same purpose as a **Message** by watching for changes
on them.  Numbers are also accessible when changing the Spawn Order or Score,
making them the most powerful memory slot.

### Spawn Order

**Spawn Orders** are sort of the cousins of **Numbers**. They can be set from
`0` to `64`. Changing the **Spawn Order** of Players will actually have an
effect on gameplay. Refer to any spawning documentation available on how they
affect gameplay. However when they aren't going to have an affect on gameplpay
(like for objects, or in gametypes/maps that don't utilize Spawn Order on
spawns), they can be a useful additional **Number** slot.

### Score

Another cousin of **Numbers**. Limits are currently unknown. Using this as a
memory slot is very risky as the core game system uses the score to indicate
losses or wins. Be very aware when you use this as a Memory slot. In a pinch,
this can serve a similar purpose as a **Message** when it changes. 

Since score also has a built in UI display, it can be used to display other 
variables, such as timers, etc., by having it mirror them. Score only displays 
for 2 teams at a time in the HUD, and can only be modified or shown for teams
that are present in the game.

### Labels

**Labels** are the closest that we get to Strings in Halo Forge. They serve as
a classification system. They are like a **Power** channel that is always on.


## Memory Available

Data can be stored in any of these Memory slots.

 - Each **Object** has its own `Number`; a sort of local variable, accessible
   under the Object scope
 - Each **Player** has `26` (**Alpha -> Zulu**) channels that store one Number;
   accessible under the Player scope
 - Each **Team** has `26` (**Alpha -> Zulu**) channels that store one Number;
   accessible under the Team scope
 - `26` (`Alpha` -> `Zulu`) shared **Number** channels that store one Number;
   accessible under the Global scope
 - `26` (`Alpha` -> `Zulu`) shared **Message** channels for broadcasting events
 - `26` (`Alpha` -> `Zulu`) shared **Power** channels which can have a value of
   On or Off
 - **Objects** & **Players** (**Entities**) can have up to `4` (`Alpha` ->
   `Delta`) **Labels** added or removed from them; exists for classification of
"Collections"
 - **Objects** & **Players** have a single **Spawn Order** Number used for
   controlling spawning
 - **Team** and **Player** **Score**, in and of itself, can serve as a Memory
   slot


## Changing Data in Memory

### Numbers

Numbers can be changed using the `Number: Change` action. The `Number: Change`
action allows you to select the **source** number, an **operator**, and a
**modifier** number.

#### Source Number Options
 - **Scope**: [`Global`, `Team`, `Player`, `Object`]
 - **Channel**: [`Alpha` thru `Zulu`]

#### Operator Options
 - `SET` - Equivalent of `=` Assignment in programming
 - `INCREMENT` - Equivalent of `+` Addition in programming
 - `DECREMENT` - Equivalent of `-` Subtraction in programming
 - `MULTIPLY` - Equivalent of `*` Multiplication in programming
 - `DIVIDE` - Equivalent of `/` Division in programming
 - `REMAINDER` - Equivalent of `%` Modulus in programming

#### Modifier Options
 - **Number Memory**
     - **Scope**: [`Global`, `Team`, `Player`, `Object`]
     - **Channel**: [`Alpha` thru `Zulu`]
 - **Constant** - From `-10,000` to `10,000`



## Detecting Changes In Memory

Messages and Power States still detected with the On Message, On Power and
Multi conditions. Messages are broadcast using the Message: Send action. Power
States are (potentially) changed using Power: Set.  Number changes will be
detected by Number: Check conditions that meet the criteria for Scope, Channel,
and operation & value the numbers get compared to. The value used to compare
can be a Constant or a Number stored in Memory which can be selected using the
Number Scope and Channel filters.  Labels aren't detected by any conditions but
players and objects that have a label can be selected by label filters as the
targets of actions that can use the new action targeting system (by hitting the
“Objects" setting or the Move action's “Target” setting).


## Changing Numbers

Numbers can be set or altered using the Number: Set action. Select the Numbers
using Action Targeting as described below. Then apply the mathematical
operation (and value used) to be performed on the Number:

 - Set
 - Addition
 - Subtraction
 - Multiplication
 - Division
 - Remainder

The value used as the math operand can be either a Constant or a Number stored
in Memory which can be selected using the Number Scope and Channel filters.


## Using Action Targeting

Up to 64 objects and players can be selected as the targets of some script
actions by using up to 8 filters.
