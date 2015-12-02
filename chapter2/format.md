# format()


### Problem
You want to convert the “Current salary” to the form of ‘###,###.##’.


### Solution
Use format() and put the desired form into the () with double quotes. 
```
node.currentsalary.format("000,000.00")
```
### Discussion
```node.currentsalary``` defines the collection you want to manipulate, here the current salary for a selected node.
The format method ```number1.format()``` puts the number into the desired form that you specify. If you don’t specify an argument, ```format()``` removes the decimal places and inserts commas in the correct place.
```node.currentsalary.format()``` will therefore give you the salary with a comma in the correct place which is 408,599 for CEO.
Specifying the form with 
```node.currentsalary.format("000,000.00") ```will return 408,599.00 as desired.