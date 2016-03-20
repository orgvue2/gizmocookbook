# Optmisation tips
## Understanding how OrgVue handles calculated data
In OrgVue, each node holds property values in 2 states - the raw value and evaluated (calculated) value. If it is detected that a property is evaluated, the value returned from that property will be the evaluated value. Otherwise, it will return the raw value.
1. The raw values are either entered manually, double splashed (!!*), copied, or uploaded from an external source, or entered via webforms
2. The evaluated values are populated through the following 3 methods:
	* The cell contains an **expression** that, once evaluated, returns a value (expression manually written out, copied in from a text editor, or !-splashed)
	* The cell is blank but has an **inherited value or expression*** that is referenced unless and until another value is inserted
	* The cell has been set via the **settemporary method** (in a 'script‘ evaluation mode)

## Optimisation tips overview
Expressions are the biggest contributor to a slow dataset, and you can mitigate this by optimising where you write expressions, how you write expressions, and how you configure them. Here are some basic tips to improve performance:
1. Write expressions in the property value box (not individual cells)
2. Write expressions as efficiently as possible - remember dots ‘.’ are expensive
3. Configure expressions so they re-calculate only as needed – appropriate use of default mode and evaluation mode
4. Use ‘settemporary’ (and ‘script’ mode) to evaluate all your properties in one 
5. Keep your tenant tidy