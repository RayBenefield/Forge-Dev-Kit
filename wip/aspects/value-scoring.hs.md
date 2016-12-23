# Value Scoring

Adds to the score based on what the order of the parent object is.
This will not score if any object in the group is **Invalid**.

 - **Labels** - **[Child]**
 - **Spawn Order** - How much the parent is worth when scoring.

| #| `HEAR` **Score**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **This.Order**|
|| `CHANGE` **This**| `MULTIPLY` **-1**|
|| `CHANGE` **This**| `MULTIPLY` **<ul><li>Count - 1 <ul><li>+This <li>+Group.Siblings <li>+[Invalid] <li>+First</ol>**|
|| `CHANGE` **<li>+This <li>+Group.siblings <li>+[Scorer]**| `SET` **This**|
