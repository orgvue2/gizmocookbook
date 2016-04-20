## Exercise Set 1

1. Find out the age of the youngest employee who directly reports to the Head of Research

2. What is the percentage of “Current Bonus” from ‘Total Annual Compensation’ for the CEO?

3. Create a new property “Bonus Percent” using the Expression used in the above question, and find out the average of each employee’s bonus percentage across the organisation 

4. What is the average “Total Annual Compensation” paid to all employees who are second level descendants to the CEO (i.e. “grandchildren”)? (tip: use node.d(x,y) notation)

5. Calculate the total days of “Absence” for a Sales director and all its descendants


## Exercise Set 2
1. Find out the average age of the organisation

2. What expression would you use to calculate bonus as a percent of total compensation in 2 decimal points

3. Find out the total payroll cost of the sales director’s direct and indirect reports

4. What expression would you use to calculate an employee’s salary as a percentage of the average salary of  their peers

5. What expression would you use to calculate the total days of absence for a team

---
### Exercise Set 1 - Answer keys
1. 41 years old. `node.c.age.min`
2. 27.5%. 
`node.math("(currentbonus/totalannualcompensation)*100")`
3. 5.7%. `nodes().bonuspercent.avg`
4. 140K. `node.d(2,2).totalannualcompensation.avg`
5. 214 days. `node.rollUp('absencedays','sum')`


