## age()
### Problem
You want to calculate age for employees using their date of birth data.

### Solution
`date1.age()` tells you how long ago a date occurred.
`node.dateofbirth.age()`


### Discussion
`age()` finds the difference between a past date and now.
So in this example `node.dateofbirth.age()` returns the difference between the date of birth and today in years for a selected node.

**Note:** When a future date is used with `age()`, a negative value is returned.

---
### Problem
You want to know the average tenure of employees in your organisation, in weeks.

### Solution
Use `age()` and put a parameter to see the value in weeks.

`nodes().rolestartdate.age('w').avg`


### Discussion
`nodes().rolestartdate.age()` yields the list of tenure values for the nodes (the number of years in current role). 
So for this in weeks, type `nodes().rolestartdate.age('w')` where the quotation marks are necessary. 
Then we average these by adding `avg` at the end: `nodes().rolestartdate.age('week').avg` - this yields 676 weeks.