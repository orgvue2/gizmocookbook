## 2. Write expressions as efficiently as possible
OrgVue expressions are written using Gizmo, a subset of JavaScript. Whilst you can’t be expected to write expressions like a developer, there are some simple rules you can follow to make your expressions quicker to run and proof check:
### Don’t repeat yourself
e.g. If referencing the same property multiple times, assign it to a variable:
``` 
if (node.appraisalgrade == “A”) then {5}
else if (node.appraisalgrade == “B”) then {4}
else if (node.appraisalgrade == “C”) then {3}
else if (node.appraisalgrade == “D”) then {2}
else if (node.appraisalgrade == “E”) then {1}
else {|}
```
vs.
```
var grade = {
   A: 5,
   B: 4,
   C: 3,
   D: 2,
   E: 1
}
grade[node.appraisalgrade]
```
### Make expressions easy to follow
e.g. Use the shorthand form of if statement (called “ternary”)
```
if (node.matrixmanagerid > 0) then {node.matrixmanagerid}
else node.linemanagerid
```
vs. 
```
node.matrixmanagerid > 0 ? node.matrixmanagerid : node.linemanagerid
```

### Try to keep up-to-date on the newest syntax
e.g. expressions like format() are frequently developed to make common functions easier and faster.
```
[node.firstname,node.lastname].join(‘ ’)
```
vs.
```
node.format(‘{firstname}{lastname}’)
```
### Bear in mind what the purpose of the expression is

** Note: ** Remember that dots ‘.’ are expensive!