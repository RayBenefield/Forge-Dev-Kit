# Attrition

Rather than weapons spawning on the map, they are replaced by weapon caches. In
order to spawn a weapon you must pay for the weapon by activating the cache
until it is ready. When the cache is ready, the next time you activate it, it will
cause the weapon to spawn.

There can only be one weapon from each cache on the map at a single moment. If
the weapon is spawned while the weapon is on the field, it will despawn, and
respawn at its original location where it was activated.

## Components

### Turn Manager

| #| `CHECK` **Game -> On**| `ALWAYS RUN`|
| ---| ---| ---|
|| `FORCE SPAWN`|
|| `CHANGE` **Turn -> On**|

| #| `CHECK` **Game -> Off**|
| ---| ---|
|| `DESPAWN`|

| #| `CHECK` **Turn -> On**|
| ---| ---|
|| `WAIT` **5.00**|
|| `CHANGE` **Turn -> Off**|
|| `WAIT` **10.00**|
|| `CHANGE` **Turn -> On**|

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

> - Label: **[Weapon]**
> - Spawn Order: Cost of Weapon initially, After **Initialization** ID

| #| `HEAR` **Weapon**| `ALWYAS RUN`|
| ---| ---| ---|
|| `FORCE SPAWN`|
|| `DESPAWN` **+[Weapon] -Activator.Order**||

---

### Cache (Powerup)

 > - Label: **[Powerup]**
 > - Spawn Order = After **Initialization** ID
 > - Boundary

| #| `CHECK` **This** < 0| `ALWAYS RUN`|
| ---| ---| ---|
|| `CHANGE` **Volatile**| `SET` **This**|
|| `CHANGE` **Volatile**| `Multiply` **-1**|
|| `ORDER CHANGE` **<li>+This.Boundary <li>+[Weapon] <li>+[TeamManager] <li>+[NavManager] <li>+This**| `SET` **Volatile**|
|| `CHANGE` **This**| `SET` **+This.Boundary +[Weapon] -> Order**|

| #| `CHECK` **This** > 0| `ALWAYS RUN`|
| ---| ---| ---|
|| `DESPAWN` **+This.Order +[Weapon]**|
|| `CHANGE` **This.Order +[NavManager] +[TeamManager]**| `SET` **0**|

| #| `CHECK` **Game -> Off** `OR` `CHECK` **Turn -> Off** `OR` `HEAR` **Initialize**|
| ---| ---|
|| `DESPAWN`|

|# | `DESPAWN`|
| ---| ---|
|| `DESPAWN` **+This.Order -[Weapon]**|

| #| `CHECK` **Turn -> On**| `ALWAYS RUN`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #| `INTERACT`||
| ---| ---| ---|
|| `CHANGE` **<li>This.Order <li>+Activator.Team <li>+[TeamManager]**| `DECREMENT` **-1**|

---

### Cache Team Manager

 > - Team
 > - Label: **[TeamManager]**
 > - Spawn Order = After **Initialization** ID
 > - **This** = Remaining

| #| `CHECK` **Turn -> On**| `ALWAYS RUN`|
| ---| ---| ---|
|| `FORCE SPAWN`|

| #| `SPAWN`||
| ---| ---| ---|
|| `CHANGE` **<li>+This.Order <li>+This.Team <li>+[NavManager]**| `SET` **This**|

| #| `CHECK` **This** < 0||
| ---| ---| ---|
|| `CHANGE` **+This**| `SET` **[Weapon.Order]**|
|| `DESPAWN` **+This.Order +[Weapon]**|
|| `SEND` **[Weapon]**|

---

### Nav Manager

 > - Team
 > - Label: **[NavManager]**

| #| `HEAR` **Urgent**||
| ---| ---| ---|
|| `CHANGE` **Volatile**| `SET` **This**|
|| `CHANGE` **This**| `SET` **-1**|
|| `CHANGE` **This**| `SET` **Volatile**|

| #| `DESPAWN`||
| ---| ---| ---|
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

