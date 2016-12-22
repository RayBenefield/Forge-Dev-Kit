# Conditional Math

There are several ways that we can use math to essentially serve as conditionals. Because multiplying by 1 results in the same value and inversely multiplying by 0 results in a 0, we can essentially do the equivalent of:

```
// If condition is false
if(result > 0) {
    // Do Stuff
} else if (result === 0) {
    // Ignore me
} else if (result < 0) {
    // Do negative things (probably with the absolute value of this)
}
```

This is extremely powerful giving us the ability to replicate having nested
conditional logic as you can respond to any event and say "if this is true, AND
we've got stuff then do this".

### Boolean Conditional - At least one object exists

This becomes more useful when you consider that we have access to counting
objects with filters. So we can say "if you send me this message and this thing
exists, then do this.' This is what it looks like:

| #1 | **{Some-Condition}**| |
| ---| ---:| :---|
|| `CHANGE` **This**| `SET` **{Default-Value}**|
|| `CHANGE` **This**| `MULTIPLY` **+Activator.Boundary +First -> Count**|
>  Do something based on **This** being 1 or 0, more validation or
transformation is a good thing to try here

### Revesrse Boolean Conditional - No objects exist

Sometimes your filters will have to result in seeing if the list is empty. If
you do this you come up with 0 and 1, but 1 is bad in this case. To get around
this we start with a negative number instead, then substract 1 from the count
to create a 0 and -1 result and then multiplying -1 by the negative default
value will result in a positive value if the list filter has nothing in it.

| #1 | **{Some-Condition}**| |
| ---| ---:| :---|
|| `CHANGE` **This**| `SET` **{Default-Value}**|
|| `CHANGE` **This**| `MULTIPLY` **-1**|
|| `CHANGE` **This**| `MULTIPLY` **+Activator.Boundary +First -> Count - 1**|
>  Do something based on **This** being 1 or 0, more validation or
transformation is a good thing to try here
