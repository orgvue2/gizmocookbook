# Gizmo idioms created by our Consultants and Developers

#### Replace currency symbols
<b>Use Case:</b> Numerical data is often not formatted appropriately when copied into OrgVue. This is because the value pasted from the clipboard is the value you see in a cell in Excel, rather than the underlying number. This can cause issues especially when your laptop is from a non-UK locale (i.e.  uses '.' instead of ',' to separate thousands) or when salary data contains currency symbols.

<b>Notes:</b> This expression will replace specified symbols (e.g. '$' in a nominated column with a specified character. Copy the expression into the Expression Manager and then switch it to Macro mode before evaluating.
```js

nodes().setproperty(n => ({'Current Salary': n.currentsalary.value.replace(/\$/g,"")}))

// replace 'Current Salary' with the (case sensitive) key of the property in question
// replace n.currentsalary with the property in question
// change $ in the replace() clause to search for another symbol

```

<b>Hints:</b> To update multiple properties at once, chain several key:values pairs together within setproperty in the same way as you would with the node.settemporary() method. For more information about the replace() syntax, see the summary of Regular Expressions (Regex) at: https://developer.mozilla.org/en/docs/Web/JavaScript/Guide/Regular_Expressions

#### Group array into a "value:count" list
###### csv
```js

array(node.resource).groupBy(i=>i).map(g=> [g.key,": ",g.values.count].join('')).join(', ')

```
###### node.d
```js

node.d.groupBy(n=>n.businesstitle).map(g=> [g.key,": ",g.values.count].join('')).join(', ')

```

#### Summarise no. blanks per property
```js

var props = view.properties.filter(p=>!p.isgenerated);


var table = props.map(k=>({name:k.name,score:1-(view.property(k).bucket('(Blank)').count/nodes().count)})).sort('score')

// View overall completeness as
array(table.score.value).sum/props.count
```

#### Convert RGB values to Hex
```js

var dd = x=>['0', Number(x).toString(16)].join('').slice(-2);

nodes().map(x=>{
  var rgb = x.rgb.value.split(',');

  return ['0x', dd(rgb[0]), dd(rgb[1]), dd(rgb[2])].join('')
}).join(', ')

// Replace "x.rgb" with x.format('{r},{g},{b}')
// if RGB values are stored in separate properties

```

#### Access Tenant back-end
###### List tenant names and IDs for which you have access
```js

[orgvue].concentra.co.uk/tenants/tenants

```

###### List recent user activity in a tenant
```js

[orgvue].concentra.co.uk/[tenantID]/requests/100

```

```js

[orgvue].concentra.co.uk/tenants/sessions

```

###### List users and their role

```js

[orgvue].concentra.co.uk/[tenant]/users

```

###### List datasets and owners

```js

[orgvue].concentra.co.uk/[tenant]/datasets

```

###### Write back end gizmo to interrogate the tenant
```js

[orgvue].concentra.co.uk/[tenant]/gizmo

// e.g. 1
resource.datasets.count

// e.g. 2
resource
.datasets
.filter(d=>d.type=="DIMENSION")
.groupby(i => i.owner)
.map(r => ({owner: r.key, numberof: r.values.count}))
.sort('numberof','desc')
```

###### Show tenant-associated tasks
```js

[orgvue].concentra.co.uk/[tenant]/tasks

```

