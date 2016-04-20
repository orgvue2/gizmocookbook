## Exercise Set 2
1. Find out the average age of the organisation

2. What expression would you use to calculate bonus as a percent of total compensation in 2 decimal points

3. Find out the total payroll cost of the sales director’s direct and indirect reports

4. What expression would you use to calculate an employee’s salary as a percentage of the average salary of  their peers

5. What expression would you use to calculate the total days of absence for a team

---
### Answer keys
1. `nodes().age.avg` 

2. `node.math("(currentbonus/totalannualcompensation*100)")`

3. `node.d.totalpayrollcost.sum`

4. `node.salary/node.s.salary.avg*100`

5. `node.rollUp("sum","absencedays")`