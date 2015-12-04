## join() 

### Problem
You want to add currency to total annual compensation by combining two existing properties; total annual compensation and ccy.

### Solution
`join()` can be used to amalgamate two or more properties.

```
[node.totalannualcompensation,node.ccy].join(" ")
```


Or simply use `format("{property} {property}")`.

```
node.format("{totalannualcompensation} {ccy}")
```


### Discussion
Define 2 or more collections you want to join in the [ ] separated by commas as in `[node.totalannualcompensation, node.ccy]`.

Note that there is a space between the two double quotes – `join(" ")`. This gives a space between two values.

When no conditional logic involved, `format()` which is simpler is preferred.