# Filter: filter()

If you want to filter the nodes according to some condition or a specific property value, the expression returns all nodes for which the condition is true.
### Generic form
```javascript
nodes().filter(n=>n[condition])
```
`n=>n` called a ‘lamda expression’ – *see '[Lamda expression](https://orgvue.gitbooks.io/gizmocookbook/content/chapter07/index.html)'*.

### Examples
1. List all the women in the organisation
`nodes().filter(n => n.gender == 'Female')`

2. List everyone without a manager or reports
`nodes().filter(n=> n.isorphan == true)`

3. List all someone’s direct reports with an engagement score less than `node.c.filter(n => n.engagement < 3)`

** Note: ** Search syntax can be nested within `filter()` for simple conditions, e.g. `nodes().filter(“gender:Female”)`. For more complicated conditions, `n=>n` and standard comparison operators are used.


