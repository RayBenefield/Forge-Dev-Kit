# Attrition

Rather than weapons spawning on the map, they are replaced by weapon caches. In
order to spawn a weapon you must pay for the weapon by activating the cache
until it is ready. When the cache is ready, the next time you activate it will
cause the weapon to spawn.

There can only be one weapon from each cache on the map at a single moment. If
the weapon is spawned while the weaponp is on the field, it will despawn, and
respawn at its original location.

## Components

### Score Manager

| #| `TIMER` 15.00|
| ---| ---|
|| `SEND` **Score**|

---

### Weapon

> Label: **[Weapon]**

| #| `CHECK` **This** >= 0|
| ---| ---|
|| `SPAWN`|

---

### Cache (Powerup)

 > Spawn Order

| #| `SPAWN`|
| ---| ---|
|| `WAIT` 5.00|
|| `DESPAWN`|

|# | `DESPAWN`|
| ---| ---|
|| `DESPAWN` **+This.Order**|

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `FORCE SPAWN`|

| #| `INTERACT`|
| ---| ---|
|| `SEND` **Activated**| `TRANSFER` **This**|

---

### Cache Team Manager

| #| `HEAR` **Initialize**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **0**|

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `FORCE SPAWN`|

| #| `SPAWN`||
| ---| ---| ---|
|| `CHANGE` **+This.Order +[NavManager]**| `SET` **This**|

| #| `HEAR` **Activated**||
| ---| ---| ---|
|| `CHANGE` **This**| `DECREMENT` **1**|

| #| `CHECK` **This** < 0||
| ---| ---| ---|
|| `CHANGE` **+This.Order +[Weapon]**| `SET` **-1**|
|| `DESPAWN` **+This.Order +[Weapon]**|
|| `CHANGE` **+This.Order +[Weapon]**| `SET` **1**|

---

### Nav Manager

| #| `HEAR` **Initialize**||
| ---| ---| ---|
|| `DESPAWN`|

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `FORCE SPAWN`|

| #| `DESPAWN`|||
| ---| ---| ---| ---|
|| `NAV` **+Players + This.Team**| `REMOVE` **+This**|
|| `CHANGE` **This**| `SET` **-1**|

| #| `CHECK` **This** = 0|||
| ---| ---| ---| ---|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **Ready**|

| #| `CHECK` **This** = 1|||
| ---| ---| ---| ---|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **1**|

| #| `CHECK` **This** = 2|||
| ---| ---| ---| ---|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **2**|

| #| `CHECK` **This** = 3|||
| ---| ---| ---| ---|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **3**|

| #| `CHECK` **This** = 4|||
| ---| ---| ---| ---|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **4**|

| #| `CHECK` **This** = 5|||
| ---| ---| ---| ---|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **5**|

---

