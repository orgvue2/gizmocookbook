## Spliting strings: split()
### Problem
You want to split full name into first name and last name.

### Solution
Use split() to break up a string at delimiter, a space for full name.

```javascript
node.fullname.value.split(" ")
```

### Discussion
`node.<property>.value.split([delimiter])` splits up a value at defined intervals – similar to performing a delimited text to columns function in Excel. 

A space or a comma are common delimiters, as in ‘Reece Harris’ from the 1505 dataset. Here you use the syntax 
`node.fullname.value.split(" ")` to split the value (string) at a space. Reece Harris will return Reece, Harris.

If the string is written in the format of ‘Harris, Reece’, `node.fullname.value.split(", ")` will be used.

Putting [index] - `node.fullname.value.split(" ")[0]` will return a substring before the delimiter – Reece for Reece Harris.

