# Spawn EventTest

**Test File**: [Spawn Event Test Map](https://www.halowaypoint.com/en-us/games/halo-5-guardians/xbox-one/map-variants?lastModifiedFilter=Everything&sortOrder=BookmarkCount&page=1&gamertag=Ray%20Benefield#ugc_halo-5-guardians_xbox-one_mapvariant_Ray%20Benefield_3b2b219c-189c-448c-9e98-266627494cb4)

 > Description


## Observations Conclusions

 > Conclusions


## Recommendations for FDK

 > Standards



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
