## Roll up calculation: rollUp()
### Problem
You want to calculate total salary of a team.

### Solution
Use `rollUp(aggregator, property)` and define the property and the aggregator.

```javascript
node.rollUp("sum","currentsalary") 
```


### Discussion:
`rollUp()` is particularly useful in the context of oranisational hierarchy as it summarises hierarchical information more efficiently than using node.d. It can be used to calculate the sum, average, count, maximum, or minimum of the property values for a node and its descendants.

`node.rollUp("sum","currentsalary")` sums up all current salaries for nodes in the hierarchy up to and including the selected node.
‘sum’ can be replaced with ‘avg’, ‘cnt’, ‘max’, ‘min’ to perform other operations depending on the situation.

`node.d.currentsalary.sum` technically does the same operation. But it’s highly inefficient as it will evaluate every node – not recommended. This will make the Dataset run slowly.

** Note: ** If you have any filters applied, this expression will perform calculations on the filtered subset of your data. If you want to do roll-up calculations on unfiltered data, use `allrollUp()` in the expression, instead of `rollUp()` e.g.  ```node.allrollUp("sum", "currentsalary")```. 
