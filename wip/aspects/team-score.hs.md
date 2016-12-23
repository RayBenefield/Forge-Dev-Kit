# Team Scoring

Adds to this team's score.

 - **Labels** - **[Scorer]**

| #| `CHECK` **This !== 0**||
| ---| ---| ---|
|| `CHANGE` **This**| `SET` **This.Order**|
|| `CHANGE` **This**| `MULTIPLY` **-1**|
|| `CHANGE` **This**| `MULTIPLY` **<ul><li>Count - 1 <ul><li>+This <li>+Group.Siblings <li>+[Invalid] <li>+First</ol>**|
|| `CHANGE` **<li>+This <li>+Group.siblings <li>+[Scorer]**| `SET` **This**|
