# Links

For the two (hierarchical) datasets which have been linked, for example roles and processes, `links` lets you answer questions such as the total number or cost of all different sets of sub-processes for which one role is responsible. 

### Problem 
You want calculate total FTEs involved in each activity when the People and the Processes datasets are linked through % time spent.

### Solution
In the Process dataset use the expression:
```javascript
node.links.value.sum
```

### Discussion
`node.links.value` lists all link values to the selected node. To calculate FTEs correctly using links, understand the format of % time spend - in percentage (0.2) or integers (20). When the values are provided in intergers, The 'total FTEs' need to be divided by 100: `node.links.value.sum/100`.

---
### Problem 
You want to calculate cost of each activity when the People and the Processes datasets are linked through % time spent.

### Solution
In the Process dataset use the expression:
```javascript
node.links.math("value*to.salary").sum
``` 
where the 'salary' property represents total payroll cost.

### Discussion
`node.links.to` lists all nodes linked to the selected node.
Further you will be able to access the specific property in the linked dataset. `node.links.to.salary` lists all 'salary' values of the nodes linked to the selected node.
To calculate the activity cost, you need to calculate '% time spend x payroll cost' for each linked node, then sum them up. 

**Node:** Be aware of the format of the link values, for example, When the values are provided in intergers, use: `node.links.math("(value/100)*to.salary").sum`.

--- 
### Problem 
You want to find the average salary of all people linked to an activity.

### Solution
In the Process dataset use the expression:
```javascript
node.links.to.currentbonus.avg
```

