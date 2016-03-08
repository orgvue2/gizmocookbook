## View statstics: stats()

### Problem
You want to calculate median salary of the whole organisation.

### Solution
Assuming the field (property) for which the median is required is Current Salary, use `nodes().stats('Current Salary').median`.

### Discussion

If you just type in `nodes().stats('Current Salary')` it will print box and whiskers plot in the Expression Pane. Adding a dot at the end `nodes().stats('Current Salary').` will list stats available for the 'Current Salary' property.


### Problem
You want to compare mean salary of female and male employees.

### Solution
When you want to perform a calculation on a subset of dataset, filter() needs to be nested in the expression. In this case, `nodes().filter(n => n.gender == 'Female').stats('Current Salary').median` and `nodes().filter(n => n.gender == 'Male').stats('Current Salary').median`.

### Discussion

[Filter chapter](https://orgvue.gitbooks.io/gizmocookbook/content/chapter6/index.html) and [Lamda expression chapter](https://orgvue.gitbooks.io/gizmocookbook/content/chapter7/index.html) explain `filter()` and `n=>n` in detail.