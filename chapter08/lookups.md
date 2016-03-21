# Lookup
`lookup` allows you to keep one or more main datasets updated with a reference set of data. This can be useful where the reference set of data needs to be updated periodically, and the change needs to be dialled through the entire population of one or more main datasets. 
The power of Lookups in OrgVue is that it allows you to normalise multiple datasets with consistent numerical values or text – or even standard images (icons, flags…) or even colours (by gender, department, etc.).

### Problem
You want to create a new property entitled 'target salary' and populate it using a lookup dataset 'grade' which contains the 'target salary' for each grade.

### Solution
```javascript
node.lookup('grade').targetsalary
```

### Discussion
This expression should give a new column 'target salary' with the target salary relative to grade. Any changes made in the lookup dataset 'grade' will automatically apply to the main dataset.

**Note:** The name the lookup dataset should be the same name as the property which will reference lookup table in the main dataset.