LiveGraph for jQuery
====================

![LiveGraph](https://raw.github.com/lampieg/LiveGraph/master/demo/inline.jpg "LiveGraph")

LiveGraph is a jQuery Plugin that allows the creation of simple bar charts from a simple JavaScript Object or an HTML table. LiveGraph allows updating of the values used to create the bar chart - by dynamically adjusting the height of the bars and rescaling the graph. Charts created with LiveGraph can easily be linked to a website's backend using AJAX to allow a graph to automatically update to display a set of data.

LiveGraphs can be customized to suit different uses, bars can be styled using CSS to change background colours / patterns and labels can have different font styles / sizes.

Demo
----
The demo is contained within the source, in the "demo" directory.

Usage
-----
LiveGraph for jQuery requires jQuery v1.7+

Data can be supplied as a HTML table.

Include jQuery as normal, then the following code needs to be added to the `<head>` section of the page you wish the graph to be shown on:
```html
<script type="text/javascript" src="jquery.livegraph.js"></script>
```
Obviously adjusting according to the directory you've saved `jquery.livegraph.js` in.

Then somewhere in `<body>` you'll want to create your graph with a bit of JavaScript:
```javascript
$('#somediv').liveGraph({
						height : 350,
						barWidth : 100,
						barGapSize : 2,
						data : 'table.dataforgraph',
						hideData : true
					});
```
Now `#somediv` should contain a graph.

Full Docs
---------

Initialising a graph:
```javascript
$('#somediv').liveGraph( settings );
```
The initial settings are set at the creation of the LiveGraph object using the settings object.
####Settings Object
Default settings are shown in brackets.
- height - integer, the maximum height for the entire chart, in pixels. (400)
- barWidth - integer, the width of each bar, in pixels. (50)
- barGapSize - integer, the spacing between bars, in pixels. (5)
- animate - boolean, where animation should be enabled. (true)
- animTime - integer, the time taken for animation to complete, in milliseconds. (2000)
- hideData - boolean, whether to hide the data table or not. (true)
- data - object OR string, the input data. If using string based CSS input, you must specify it as "table#id" or "table.class". (object based demo values)

####Data Object
Here's a sample data object:
```javascript
var data = {
  bar1: {
    label: "Bar 1",
    value: 2
  },
  bar2: {
    label: "Bar 2",
    value: 1
  },
  bar3: {
    label: "Bar 3",
    value: 3
  }
}
```
You can specify as many bars as you wish, there is no limit. Obviously this will determine the overall graph's width.

The table method will assume that the first column contains labels, and the second column values. It will create an object naming each bar as "tb#" where # is the bar number.

####Updating the Graph
With a pre-existing graph, you can update the labels and / or values simply by re-issuing a data object.
```javascript
$('#somediv').liveGraph('update', data);
```
When updating the data object can be shortened for ease so that only data that is to be updated is actually needed. Shown here:
```javascript
var data = {
  bar1: 5,
  bar2: {
    label: "New Label"
  },
  bar3: {
    value: 7
  }
}
```
All these will be correctly interpretted, as well as the original per-bar object method.

####Changing Settings after Initialise
All settings can be accessed and modified using
```javascript
$('#somediv').data('liveGraph').settings
```
For example, to disable animation:
```javascript
$('#somediv').data('liveGraph').settings.animate = false;
```

__Updating graph data in this way will not work, please use the "update" method.__

Styling
-------
View the "livegraph.css" file in the demo directory for a starting point for styling.

The graph itself is created using divs with the following classes:
- liveGraph
- bars
- bar

To access the bar itself, for setting backgrounds etc, you will need to use the `span` inside each `div.bar`.

Some properties may not seem to work, this is because the plugin uses some inline `style` attributes, so any border rules will need to override the inline properties. Eg:
```css
div.liveGraph div.bars div.bar span {
  border:none !important;
}
```
