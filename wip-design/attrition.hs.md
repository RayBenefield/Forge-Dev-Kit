# Attrition

Rather than weapons spawning on the map, they are replaced by weapon caches. In
order to spawn a weapon you must pay for the weapon by activating the cache
until it is ready. When the cache is ready, the next time you activate it will
cause the weapon to spawn.

There can only be one weapon from each cache on the map at a single moment. If
the weapon is spawned while the weaponp is on the field, it will despawn, and
respawn at its original location.

## Components

### Turn Manager

| #| `CHECK` **Game -> On**|
| ---| ---|
|| `FORCE SPAWN`|

| #| `CHECK` **Game -> Off**|
| ---| ---|
|| `DESPAWN`|

| #| `TIMER` **15.00**|
| ---| ---|
|| `CHANGE` **Turn -> On**|

| #| `CHECK` **Turn -> On**|
| ---| ---|
|| `WAIT` **5.00**|
|| `CHANGE` **Turn -> Off**|

---

### Urgent Manager

| #| `CHECK` **Turn -> On**|
| ---| ---|
|| `WAIT` **1.00**|
|| `SEND` **Urgent**|
|| `WAIT` **1.00**|
|| `SEND` **Urgent**|

| #| `CHECK` **Turn -> On**|
| ---| ---|
|| `WAIT` **3.00**|
|| `SEND` **Urgent**|
|| `WAIT` **1.00**|
|| `SEND` **Urgent**|

---

### Weapon

> Label: **[Weapon]**

| #| `CHECK` **This** >= 0|
| ---| ---|
|| `SPAWN`|

---

### Cache (Powerup)

 > Label: **[Powerup]**
 > Spawn Order = Initially Cost, After **Initialization** ID
 > Boundary

| #| `HEAR` **Initialize**||
| ---| ---| ---|
|| `CHANGE` **+[Weapon]**| `SET` **-1**|
|| `DESPAWN`|

| #| `CHECK` **This** < 0| `ALWAYS RUN`|
| ---| ---| ---|
|| `CHANGE` **Volatile**| `SET` **This.Order**|
|| `ORDER CHANGE` **+This**| `MULTIPLY` **-1**|
|| `ORDER CHANGE` **+This.Boundary +[Weapon] +[TeamManager] +[NavManager]**| `SET` **This.Order**|
|| `CHANGE` **This**| `SET` **Volatile**|

| #| `CHECK` **Game -> Off**|
| ---| ---|
|| `DESPAWN`|

| #| `CHECK` **Turn -> Off**|
| ---| ---|
|| `DESPAWN`|

|# | `DESPAWN`|
| ---| ---|
|| `DESPAWN` **+This.Order**|

| #| `CHECK` **Turn -> On**| `ALWAYS RUN`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #| `INTERACT`|
| ---| ---|
|| `SEND` **Activated**| `TRANSFER` **This**|

---

### Cache Team Manager

 > Label: **[TeamManager]**
 > Spawn Order = After **Initialization** ID
 > **This** = Remaining

| #| `HEAR` **Initialize**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **0**|

| #| `CHECK` **Turn -> On**||
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
|| `CHANGE` **+This**| `SET` **[PowerUp]**|
|| `CHANGE` **+This.Order +[Weapon]**| `SET` **-1**|
|| `DESPAWN` **+This.Order +[Weapon]**|
|| `CHANGE` **+This.Order +[Weapon]**| `SET` **1**|

---

### Nav Manager

> Label: **[NavManager]**

| #| `HEAR` **Urgent**|||
| ---| ---| ---| ---|
|| `CHANGE` **Volatile**| `SET` **This**|
|| `CHANGE` **This**| `SET` **-1**|
|| `CHANGE` **This**| `SET` **Volatile**|

| #| `DESPAWN`|||
| ---| ---| ---| ---|
|| `NAV` **+Players + This.Team**| `REMOVE` **+This**|
|| `CHANGE` **This**| `SET` **-1**|

| #| `CHECK` **This** = 0| `ALWAYS RUN`||
| ---| ---| ---| ---|
|| `FORCE SPAWN`|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **Ready**|

| #| `CHECK` **This** = 1| `ALWAYS RUN`||
| ---| ---| ---| ---|
|| `FORCE SPAWN`|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **1**|

| #| `CHECK` **This** = 2| `ALWAYS RUN`||
| ---| ---| ---| ---|
|| `FORCE SPAWN`|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **2**|

| #| `CHECK` **This** = 3| `ALWAYS RUN`||
| ---| ---| ---| ---|
|| `FORCE SPAWN`|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **3**|

| #| `CHECK` **This** = 4| `ALWAYS RUN`||
| ---| ---| ---| ---|
|| `FORCE SPAWN`|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **4**|

| #| `CHECK` **This** = 5| `ALWAYS RUN`||
| ---| ---| ---| ---|
|| `FORCE SPAWN`|
|| `NAV` **+Players +This.Team**| `TARGET` **+This**| `TEXT` **5**|

---

