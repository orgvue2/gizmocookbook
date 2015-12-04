## math()

### Problem
You want to know “Total compensation” of each employee by adding “Salary” and “Bonus”.


### Solution
Use math() and insert the formula using common arithmetical operators in the bracket with double quotes.

```
node.math("currentsalary+currentbonus")

```

### Discussion

```math()``` is one of the most frequently used expressions. It allows you to create a new property by performing calculations on the existing properties – in this example, “Total compensation”.

** Note: ** ```math()``` can’t work with relationship properties such as c, s, p and d. When you need to perform calculations involving relationships, e.g. when you want to calculate an employee’s salary as a percentage of the average salary of  their peers, use 
```node.salary/node.s.salary.avg*100```

---
### Problem
You want to calculate the percentage of “Benefits” to “Total annual compensation” in the format of 0.00.

### Solution
Use math() operation and common arithmetical operators, for this example: 

node.math("(totalbenefits/totalannualcompensation)*100").format("0.00")

### Discussion
node.math("totalbenefits/totalannualcompensation") will return the proportion to 17 decimal places, 0.07237965… for CEO.

Multiplying it by 100 will convert it to percentage, 7.237965… 

Putting format() at the end lets you shorten the value into the desired form, e.g. format(“0.00”) will return 7.20.
