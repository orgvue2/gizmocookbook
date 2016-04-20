## Exercise Set 3
1. What expression would you use to display full name and role title joined by ‘-’ (dash), e.g. Reece Harris - CEO

2. Create a new property which holds the first 3 characters of Department only

3. Create 2 properties First name and Last name from Full name in the 1505 dataset

---
### Answer keys
1. `node.format("{fullname} - {role} ")` 
or `[node.fullname,node.role].join("-")`

2. `node.department.value.slice(0,3)`

3. First name:  `node.fullname.value.split(" ")[0]`
Last name:  `node.fullname.value.split(" ")[1]`

