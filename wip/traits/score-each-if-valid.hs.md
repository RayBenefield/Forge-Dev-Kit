# Score Each if Valid

Adds **1** to the score for every object in the parent's boundary.
This will not score if any object in the group is **Invalid**.

 - **Labels** - Whatever object type needs to be scored.

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **<ul><li>Count -1 <ul><li>+Activator.Boundary <li>+This.Labels**|
|| `CHANGE` **This**| `MULTIPLY` **<ul><li>Count - 1 <ul><li>+This <li>+Group.Siblings <li>+[Invalid] <li>+First</ol>**|
|| `CHANGE` **<li>+This <li>+Group.siblings <li>+[Scorer]**| `SET` **This**|
