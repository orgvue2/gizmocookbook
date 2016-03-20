## Formatting strings: format()
### Problem
You want to add ‘years’ at the end of tenure years. 

### Solution
Use `format()` and define the format you want to print out using {property name} and text.

`node.format("{tenureyears} years")`

### Discussion
`format()` method can work both for numbers and strings (text).

You can define a desired format combining properties and words within double quotes – here one property and one word.

Putting the property name within `{ }` returns the value for that property for the current node. 
A space between {tenureyears} and “years” prints out a space.