# math()

### Problem
You want to know “Total compensation” of each employee by adding “Salary” and “Bonus”.


### Solution
Use math() and insert the formula using common arithmetical operators in the bracket with double quotes.

```
node.math("currentsalary+currentbonus")

```

### Discussion

```math()``` is one of the most frequently used expressions. It allows you to create a new property by performing calculations on the existing properties – in this example, “Total compensation”.

Note:
```math()``` can’t work with relationship properties such as c, s, p and d. When you need to perform calculations involving relationships, e.g. when you want to calculate an employee’s salary as a percentage of the average salary of  their peers, use 
```node.salary/node.s.salary.avg*100```
