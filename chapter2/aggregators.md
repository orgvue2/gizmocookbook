## Aggregators (sum, avg, cnt)
### Problem
You want to calculate total amount paid out as bonuses.

### Solution
Specify the collection and add an aggregator, e.g. ‘sum’.

nodes().currentbonus.sum


### Discussion
```nodes().currentbonus``` specifies the collection on which you want to perform the operation – “Current bonus” for all employees.
Putting ‘sum’ after the collection will add all numbers within the collection and return the result as one number – 8541249 in the 1505 Dataset.
It can be formatted as 8,541,249 by putting `format("")` at the end of the syntax.

** Note:** The operations such as sum, avg, cnt are called ‘aggregators’ because they aggregate the many values in the defined collection into one number. Note that aggregators only work for numerical properties. 


- - -


### Problem
You want to calculate average “Performance ranking” of a manager’s direct reports.

### Solution
Specify the collection and add an aggregator ‘avg’.
```node.c.performanceranking.avg```


### Discussion
```node.c.performanceranking.avg``` defines the collection you want to perform an operation, i.e. performance ranking of the children of the selected node.
A aggregator avg will take the averages of all the values (performance ranking) in the collection and return it – 5.016666… for CEO.

- - -

### Problem
You want to see the possible entries for “Hours worked per week”.

### Solution
Use distinct.cnt.

`nodes().hoursworkedperweek.distinct.cnt`

### Discussion
```nodes().hoursworkedperweek``` will return the list of hours per week for whole organisation.
```nodes().hoursworkedperweek.cnt``` will count the values within the defined collection – 1505.
```nodes().hoursworkedperweek.distinct``` returns same collection without repeated values – 40, 25, 30.
Then ```nodes().hoursworkedperweek.distinct.cnt``` counts the distinct values in the collection – 3. 

**‘cnt’ vs. ‘count’**
* cnt only counts numbers in the collection 
* count is the length of the collection, i.e. total count of values whether they are numbers or not