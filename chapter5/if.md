## If statement: if()
### Problem
You want to know who are reaching close towards the retirement age and possible leave the company in near future.

### Solution
Use if(){} else if(){} else{}:
```
if (node.age > 55) {"Risk"}
else {"No Risk"}
```


Or shorten the syntax using a ? b : c (ternary) syntax.

```
node.age > 55 ? "Risk" : "No Risk"
```


### Discussion
Generic form for conditional logic is `if (condition) {return value}`.

As a general rule, '{}' denotes the parts of expressions to be executed - the ‘then’ part that is returned when the condition is met, e.g. `if (node.age > 55) {“Risk"}`; this will return Risk if the age of the current node is over 55.

Including `else {}` adds a contingency. In this example, if the current node (employee) is 55 or younger than 55, No Risk will be returned.

`a? b: c` can replace `if(){} else{}`.

** Note: ** Use operators to add nuance to the condition, e.g. `if (node.country == "UK“ && node.depth < 3) {"UK Management"}`.

---

### Problem
You want to classify performance ranking data; 8-10 as A, 6-8 as B, 4-6 as C and 0-4 as D. 

### Solution
(1)
```
if(node.performanceranking > 8) {“A”}
else if(node.performanceranking > 6) {“B”}
else if(node.performanceranking > 4) {“C”}
else {“D”}
```

(2)
```
var pr = node.performanceranking
if(pr > 8){"A"}
else if(pr > 6){"B"}
else if(pr > 4){"C"}
else{"D"} 
```

### Discussion
You can build expressions nesting multiple `else if {}` as in (1).

However, this is an inefficient approach as it evaluates the node multiple times for the same operation which causes performance loss – *This will be discussed further in the ‘Optimising tips’chapter*. In (2) var (variable declaration) connects value to the reference so the expressions can refer to the value without repeating evaluation. Note that `node.performanceraking` has been only used once in (2) while it has been used 3 times in (1)

