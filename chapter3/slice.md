## slice()
### Problem
You want to take the ‘£’ off a list of salary data.

### Solution
Use slice() to return a sub string of text.
```
node.salary.value.slice(1)
```


### Discussion
Generic form is `node.<property>.value.slice([index1], [index2])` and it returns the text block from the first index (inclusive) to the second index (exclusive) of the property.

Putting ‘value’ is to extract the raw value from the collection. 

The first character in the block is index = 0.

Missing out the stop index [index2] will return the rest of the text. So `node.salary.value.slice(1)` will return 100000 for £1000000.