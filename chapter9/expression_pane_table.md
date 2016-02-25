# Expression Pane tables

## What are expression pane tables?

Expression pane tables are a new and growing feature of OrgVue. Recently the OrgVue team have been designing expressions that, when evaluated, generate a mini table in the returns pane. An existing example of this capability is the stats table, e.g.
```js
nodes().stats('total_cost').transpose
```
Currently we have developed around a dozen of these ‘array/table expressions’.

## Why use expression pane tables?

The aim of these tables is to enhance the user’s OrgVue experience. Expression pane tables have been developed for a number of use cases, e.g.
* Summarising the changes that have been made since the last save
* Showing various measures of data quality
* Aggregating data across chosen measures/dimensions

OrgVue already contains ways of getting these insights, e.g. Filter control, dashboards.

However, there are 4 main advantages of using expression pane tables, they:
1. Display information without having to switch screens  - helpful when making multiple changes
2. Remain up-to-date without needing to recalculate (unlike the filter control)
3. Can be copied out into Excel
4. Can be customised by the user to query the dataset in specific ways

Expression tables can also be easily saved. To avoid users having to type out the whole expression, they are declared as ‘global’ expressions:

```js
global.changes = function(nd){array(
{
  "Change":"Node(s) added",
  "Count":global.changeCount("created")
},
{
  "Change":"Node(s) updated",
  "Count":global.changeCount("updated")
},
{
  "Change":"Node(s) deleted",
  "Count":global.changeCount("deleted")
});
};
global.changeCount = function(actionType){
view.changeset()._action.filter(c=>c==actionType).count;};
```

This has 2 main consequences:
* Expression pane tables can be generated simply by typing the global expression name: global.changes()
* Expressions can be stored in useful ways.

You will notice that there is another global expression nested inside the one above, which is also useful.

## Example expression tables

### Find non-generated properties
* Name: `global.properties()`
* Script:
```js
global.properties = function(){
    view.properties.filter(p=>!p.isgenerated);
};
```
Note: Can be modified to:
    - add `.sort('type','desc')` to sort by Data Type
    - add `.sort('name',’asc')` to sort alphabetically


* What it does: Lists all the non-generated properties in the dataset
* When use it: a) Quick review of a dataset's properties without having to scroll through the Properties Pane/ Filter Control/  Side Panel
b) Pasting dataset properties out of OrgVue without having to delete nodes



### View the node changes since last save
* Name: `global.changes()`
* Script:
```js
global.changeCount = function(actionType){
view.changeset()._action.filter(c=>c==actionType).count;
};
global.changes=function(nd){
array(
{
"Change":"Node(s) added",
"Count":global.changeCount("created")
},
{
"Change":"Node(s) updated",
"Count":global.changeCount("updated")
},
{
"Change":"Node(s) deleted",
"Count":global.changeCount("deleted")
}
);
};
```
* What it does: Lists the changes made since last save (Throws an error if no changes have been made)
* When use it: Making multiple changes to a dataset without needing a refresh (unlike filter control)


### Summarise RAG status in an objectives dataset
* Name: `global.rag()`
* Script:
```js
// RAG status statistics (if applicable)
global.rag = function(property) {
nc = nodes().count;
view.property('current_rag').buckets.map(b =>
{
bc = b.items.count;
return {
        " ": b.name,
        count: bc,
        percent: array(bc / nc * 100).format("0.00").value.concat("%")
            }
}).concat({
        " ": "Total",
        count: nc,
        percent: "100.00%"
})
};
```
* What it does: Shows RAG status statistics (if applicable) - filter-dependent. (Throws an error if the dataset does not contain a property called ‘current_rag’).
* When use it: Quick numerical summary of RAG status without recalculating/having to leave worksheet

### Summarise data quality

* Name: `global.dataQuality()`
* Script:
* ```js
global.dataQuality=function(nd){
nc = nodes().count;
topLevel = nodes().filter(n=>n.depth==1);
oc = nodes().filter(n=>n.isorphan==true).count;
array(
{" ":"Records","Count":nodes().count},
{" ":"In main structure","Count":topLevel.map(n=>n.d(0).count).max},
{" ":"Blank parent ID","Count":topLevel.count-1},
{" ":"Orphan groups","Count":topLevel.count-oc-1},
{" ":"Orphans","Count":oc},
{" ":"Duplicate IDs","Count":nodes().isduplicate.filter("true").count},
{" ":"Completeness Score","Count":"TBC"}
);
};
```
* What it does: Overviews completeness and quality of the data (Completeness score to be defined). Shows mostly the same metrics as the Data Types and Patterns dashboard but in an Excel-friendly format
* When use it: Review changes to data quality whilst in worksheet
Output numerical summary of dataset quality into Excel


### See high-level dataset meta-data

* Name: `global.dataSummary()`
* Script:
```js
global.properties = function(){
view.properties.filter(p=>!p.isgenerated);
};
global.propertyCount = function(thisProperty){
global.properties().filter(p=>p.type==thisProperty).count
};
global.dataSummary=function(nd){
nc = nodes().count;
array(
{" ":"Nodes","Count": array(nc).format()},
{" ":"Properties","Count":global.properties().count},
{" ":"Cells","Count":array(nc*global.properties().count).format()}
).concat(array(
{" ":" ","Count":" "},
{" ":"Dimensions","Count":global.propertyCount("text")},
{" ":"Measures","Count":global.propertyCount("number")},
{" ":"Dates","Count":global.propertyCount("date")},
{" ":"Booleans","Count":global.propertyCount("boolean")}
));
};
```
* What it does: Lists number of nodes and properties; data size and shape (per type)
* When use it: For a brief look at the type of data in the dataset - data type, # nodes and properties, without having to use dashboards or filter control
Output numerical summary of dataset into Excel

### View variance of specified property

* Name: `global.mathMoments(nodes().<propertyInQuestion>)`
* Script:
```js
global.mathMoments = function(anyProperty){
n = nodes().count;
mean = anyProperty.sum/n;
variance = anyProperty.map(i => Math.pow((i - mean),2)).sum/(n-1);
stdev = Math.sqrt(variance);
skew = anyProperty.map(i => Math.pow((i - mean),3)).sum/((n-1)*Math.pow(stdev,3));
kurtosis = anyProperty.map(i => Math.pow((i - mean),4)).sum/((n-1)*Math.pow(stdev,4));
array(
{"Moment":"M1: Mean","Value":array(mean).format()},
{"Moment":"M2: Variance","Value":array(variance).format()},
{"Moment":"M3: Skew","Value":array(skew).format()},
{"Moment":"M4: Kurtosis","Value":array(kurtosis).format()}
).concat(
array(
{"Moment":"","Value":""},
{"Moment":"Std Dev","Value":array(stdev).format()},
{"Moment":"N","Value":array(n).format()}
)
);
};
```
* What it does: Shows the mathematical moments of defined property (statistics of Variance)
* When use it: Need to calculate statistical variance

### View what global expressions there are

* Name: `global.list()` || `global.listFull()`
* Script:
```js
global.list = function(){
return array(
{"global":".list()","summary":"Lists all global.expressions()"},
{"global":".changes()","summary":"Node changes since last save"},
{"global":".rag()","summary":"RAG status stats (if applicable) "},
{"global":".dataQuality()","summary":"Summarises dataset"},
{"global":".dataSummary()","summary":"Dataset size and shape"},
{"global":".mathMoments()","summary":"nodes().myProperty Mathematical moments"}
);
};
```
* What it does: Lists all these expressions (listFull includes descriptions)
* When use it: Wanting to use one of these expressions without consulting external resource
