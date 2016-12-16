# Timer Pattern Test

**Test File**: [Timer Pattern Test Map](https://www.halowaypoint.com/en-us/games/halo-5-guardians/xbox-one/map-variants?lastModifiedFilter=Everything&sortOrder=BookmarkCount&page=1&gamertag=Ray%20Benefield#ugc_halo-5-guardians_xbox-one_mapvariant_Ray%20Benefield_7817e8b0-d9ae-473c-9e82-62027228a22e)

When the design docs from 343 were given to us, I noticed two different
patterns for repeated timers being used. The first was a timer that used the
`TIMER` **X.XX** condition to trigger an action. We'll refer to this as the
`Repeat Timer`. The second was a timer that would send an initial
**Message** on becoming active, and then use a condition of `HEAR` **Message**,
`WAIT` **X.XX**, then `SEND` **Message** to re-trigger the cycle. We'll refer
to this as the `Wait Timer`.

While deciding how to handle timers on a standardized scale, information on
which pattern to use was essential. This test helps demonstrate and analyze the
two different patterns side-to-side.


## Observations Conclusions

So it looks like both patterns have their uses for sure, which explains why
they both exist on their KoTH design.

The `Repeat Timer` happened to be really consistent over short repeat
intervals. It remained steady and didn't seem to skip a beat at all. This was
easily seen over the **0.1** and **1.0** intervals. The monitor colors remained
steady... so much so that the **0.1** monitor didn't actually lose its color...
ever. I thought it was broken several times and had to check and re-check the
scripts. When it came to longer periods though, it seemed to lose accuracy and
was heavily affected by network lag. Perhaps the `TIMER` is tied to a
synchronized network clock on the dedicated server. Who knows, what matters is
that when you wanted it to hit the **5.0** or **10.0** second intervals on the
Round clock consistently, the `Repeat Timer` just didn't fulfill that need.

The `Wait Timer` was the exact opposite. In the short repeat intervals, it
proved to be inconsistent, seemingly skipping beats every once in a while. You
can visually see the monitor of the `Wait Timer` constantly blinking next to
the `Repeat Timer`, that was staying a steady green. It was less obvious with
the **1.0** interval, but when you observed it in isolation it felt off in
comparison to the timer, like it lost accuracy for every re-trigger. In the
longer intervals though, it really shined. It matched the Round Clock almost on
the dot every single time. After about 7 minutes, you could notice a slight
lag, but it wasn't enough to make a huge difference perhaps unless you are a
pro player relying on the Round Clock. It also started exactly when the Round
Started, the `Repeat Timer` was inconsistent, sometimes a tad off, other times
being 2-3 seconds off (sometimes firing on number 8 rather than 5 in the case
of the **5.0** interval).


## Recommendations for FDK

What does this mean for the FDK standards?

 - If you are trying to implement a **Heartbeat** of less than **1.0** seconds,
   then DEFINITELY go with the `Repeat Timer`. This will ensure constant
updating for things like UI, constant move offset objects, etc.

 - If you are going with a **1.0** second timer for something like King of the
   Hill scoring, then either should work fine. The `Repeat Timer`'s lack of
long term accuracy is not really noticeable, and the `Wait Timer` doesn't skip
any beats at a rate of **1.0** (unlike lower intervals). 343 uses the `Wait
Timer` for their KoTH scoring.

 - If you are going for anything more than **1.0** seconds, especially if you
   are wanting to sync up with the Round Clock, then DEFINITELY use the `Wait
Timer`. Intervals like **5.0**, **10.0**, **60.0**, etc. seconds are MUCH more
accurate over the long term with the `Wait Timer` and allows reliance on the
Round Clock. The more the message is resent, the more inaccurate it is, so just
be aware of that.



## Scripts under Test

| Variable| 1| 2| 3| 4|
| ---| ---| ---| ---| ---|
| **Interval**| 0.1| 1.0| 5.0| 10.0|
| **Repeat Channel**| Alpha| Charlie| Echo| Juliet|
| **Wait Channel**| Bravo| Delta| Foxtrot| Kilo|

---

> Repeat Timer

| #1| `CHECK` **Game -> On**| `ALWAYS RUN`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #2| `TIMER` **Interval**|
| ---| ---|
|| `SEND` **Repeat Channel**|

| #3| `CHECK` **Game -> Off** `OR` `HEAR` **Initialize**| `ALWAYS RUN`|
| ---| ---| ---|
|| `DESPAWN`|

---

> VS

---

> Wait Timer

| #1| `CHECK` **Game -> On**| `ALWAYS RUN`|
| ---| ---| ---|
|| `FORCE SPAWN`|
|| `SEND` **Wait Channel**|

| #2| `HEAR` **Wait Channel**|
| ---| ---|
|| `WAIT` **Interval**|
|| `SEND` **Wait Channel**|

| #3| `CHECK` **Game -> Off** `OR` `HEAR` **Initialize**| `ALWAYS RUN`|
| ---| ---| ---|
|| `DESPAWN`|

---
