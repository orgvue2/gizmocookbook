# Custom dimensions/ Custom filters

## What are custom dimensions?
A custom calculated dimension is a property created by the user that only exists within the **filter** and **pagination** controls. The user can write a list of criteria to define which nodes are placed into which value bins.

Unlike most filters, the same node can exist in multiple bins. This allows the rules to be complex, and makes custom dimensions a perfect tool for supporting org charts.

The criteria can be defined, for example, to create an org chart for every manager in the business containing their line manager (‘parent’) and two levels below them. This allows for automation of common org charting requirements and greatly decreases time and effort required to produce them.

## How do you create custom dimensions?
A custom dimension is defined via a Gizmo script (containing OrgVue expressions).
When evaluated, these scripts generate the custom dimension.

#### Custom dimension scripts are diverse, but all have a common structure:
```js
/** {"name":"Org Chart Dimension"} */
api.register({
   type: "dimension",
   name: "Org",
   start: function(event) {
	return event.nodes
	.filter(n=>n.isleaf==false)
	.map(n=>({name: n._label, entries: n.ad(-1,2)}))
   }
});
```
To break this down, the first line Defines the name of the Script for reference:
```js
/** {"name":"Org Chart Dimension"} */
```
The next 2 lines are commands telling OrgVue that you would like to define a custom dimension:

```js
api.register({
   type: "dimension",
```

You then specify the name that will appear in the filter control :

```js
name: "Org",
```

Lines 5 and 6 flag the beginning of the custom filter function:

```js
start: function(event) {
return event.nodes
```

From here, we can define what the custom dimension will actually do. In this case:

```js
event.nodes // getting all the nodes
.filter(n=>n.isleaf==false) // filtering out the leaves, ie keep managers only
.map(n=>({name: n._label, entries: n.ad(-1,2)})) // and including parent and 2 levels down
```

#### How to add multiple bins to the custom filter
You can extend a custom dimension to contain multiple bins. To do this, you will add lists of name:entries pairs in { }.

Here is an example:

 ```js
 /** {"name":"Report Filters"} */
api.register({
   type: "dimension",
   name: "Report Filters",
   start: function(event) {
      return [{
      name: "All UK/RI Employees",
      entries: event.nodes.filter(n => n.businessunit == "UK" ||
         n.location == "Dublin")
  }, {
      name: "All Other EU Employees",
      entries: event.nodes.filter(n => n.businessunit == "EU" &&
         n.location != "Dublin")
       }
   ]}
});
```

In each {}, `name` defines the name of this to-be category of nodes
 and `entries` sets the filter to the nodes meeting the criteria of this category.

NB. Make sure to match up all your brackets

* Use parentheses `()` for any expression parameters
* Use curly braces `{}` for each filter category
* Use square braces `[]` for enclosing the return statement

## Examples of custom dimension scripts

### Active positions based on month
```js
/** {"name":"Active Positions"} */
api.register({
	type: "dimension",
	name: "Active Position Filter",
	start: function(event) {
		return [{
			name: "2014-01 active roles",
			entries: event.nodes.filter(n => n.positionstartdate.diff(date(2014, 1, 31)) < 0 && n.positionstartdate.value != (Blank) && n.positionenddate.diff(date(2013, 12, 31)) > 0)
		}, {
			name: "2014-02 active roles",
			entries: event.nodes.filter(n => n.positionstartdate.diff(date(2014, 2, 28)) < 0 && n.positionstartdate.value != (Blank) && n.positionenddate.diff(date(2014, 1, 31)) > 0)
		}, {
			name: "2014-03 active roles",
			entries: event.nodes.filter(n => n.positionstartdate.diff(date(2014, 3, 31)) < 0 && n.positionstartdate.value != (Blank) && n.positionenddate.diff(date(2014, 2, 28)) > 0)
		}, {
			name: "2014-04 active roles",
			entries: event.nodes.filter(n => n.positionstartdate.diff(date(2014, 4, 30)) < 0 && n.positionstartdate.value != (Blank) && n.positionenddate.diff(date(2014, 3, 31)) > 0)
		}, {
  etc.
      }]
	}
});
```

### Check the quality of your hierarchy
```js
/** {"name":"Hierarchy Validator"} */

api.register({
    type: "dimension",
    name: "Hierarchy Validator",
    start: function(event) {
        var roots = new Object(); //root lookup
        var maxRootDesCnt = 0; //highest count of descendents
        var maxRootID, rt, curRollup;
        var pID = view.parentid.value;
        event.nodes
            .foreach(nd => {
                rt = nd.root;
                if(!roots.hasOwnProperty(rt._id.value)){
                    curRollup = rt.allrollup('_records','sum').value;
                    if(maxRootDesCnt < curRollup){ //if current root has most descendents so far
                        maxRootDesCnt = curRollup;
                        maxRootID = rt._id.value;
                    };
                }
                roots[nd._id.value] = rt._id.value; //cache all roots against id
            });
            this.test = roots;
            this.test2 = maxRootID;
        return event.nodes
            .groupby(nd => global.classifyNode(nd), 'name', 'entries');
    }
});

global.classifyNode = function(nd){
    if(roots[nd._id.value] === maxRootID){
       return "In main org";
    }
    if(nd._isorphan.value){
        if(nd[pID].isblank){
            return "Orphan with blank PID";
        }
        return "Orphan with invalid PID";
    }
    if(nd.depth.value === 1){
        return "Head of orphan group";
    }
    return "In orphan group";
}


```
### Split a CSV list into its component parts
```js
/** {"name":"CSV Contains Filter"} */

api.register({
	type: "dimension",
	name: "CSV Contains",
	start: function(event) {
		return event.nodes.groupby("committee_member", "name", "entries").to_a
	}
})
```