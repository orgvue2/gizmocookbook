## Answer keys

## Exercise Set 1
1. 41 years old. `node.c.age.min`
2. 27.5%. 
`node.math("(currentbonus/totalannualcompensation)*100")`
3. 5.7%. `nodes().bonuspercent.avg`
4. 140K. `node.d(2,2).totalannualcompensation.avg`
5. 214 days. `node.rollUp('absencedays','sum')`

## Exercise Set 2
1. `nodes().age.avg` 

2. `node.math("(currentbonus/totalannualcompensation*100)")`

3. `node.d.totalpayrollcost.sum`

4. `node.salary/node.s.salary.avg*100`

5. `node.rollUp("sum","absencedays")`


## Exercise Set 3
1. `node.format("{fullname} - {role} ")` 
or `[node.fullname,node.role].join("-")`

2. `node.department.value.slice(0,3)`

3. First name:  `node.fullname.value.split(" ")[0]`
Last name:  `node.fullname.value.split(" ")[1]`

## Exercise Set 4
1. 
`date(2015,10,02).diff(date(2012,08,09))` = 1149
`date(2015,10,02).diff(date(2012,08,09),’w’)` =164.14 `date(2015,10,02).diff(date(2012,08,09),’m’)` =37.77
`date(2015,10,02).diff(date(2012,08,09),’y’)` = 3.15

2. `date(2016,04,01).diff(today())`

3. Age of the CEO: `node.dateofbirth.age()` 
Average age of the company: `nodes().dateofbirth.age().avg`

## Exercise Set 5
1. `node.bradfordindex > 100 ? "Risk" : "No Risk "` 
or `if (node.bradfordindex>100) {"Risk"} else {"No Risk"}`

2. `if(node.depth == 3 && node.isleaf==false) {"Middle Management"} else {"Other"}`

3. `if(node.currentsalary>150000) {"High"} else if(node.currentsalary > 50000) {"Medium"} else {"Low"}`

