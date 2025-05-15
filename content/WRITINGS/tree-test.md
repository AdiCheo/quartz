---
title: "Tree test"
alias: "tree-test"
feature_image: "nan"
type: "post"
status: "published"
visibility: "public"
modified: "2020-12-05T17:55:32.000Z"
---

<p>This post is not about writing... just testing how I can visualize links to other pages using diagrams</p><!--kg-card-begin: html-->
    <script
      type="text/javascript"
      src="https://unpkg.com/vis-network/standalone/umd/vis-network.min.js"
    ></script>
    <script
      type="text/javascript" 
      src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.24.0/moment.min.js"
    ></script>
    <script
      type="text/javascript"
      src="https://visjs.github.io/vis-timeline/standalone/umd/vis-timeline-graph2d.min.js"
    ></script>
    <style type="text/css">
      #mynetwork {
        width: 600px;
        height: 400px;
        border: 1px solid lightgray;
      }
    </style>
  </head>
  <body>
    <div id="mynetwork"></div>
      
    <script type="text/javascript">
      
        
        // create an array with nodes
var nodes = new vis.DataSet([
  { id: 1, label: "Node 1" },
  { id: 2, label: "Node 2" },
  { id: 3, label: "Node 3" },
  { id: 4, label: "Node 4" },
  { id: 5, label: "Node 5" },
  { id: 6, label: "Node 6" },
  { id: 7, label: "Node 7" },
  { id: 8, label: "Node 8" },
]);

// create an array with edges
var edges = new vis.DataSet([
  { from: 1, to: 8, arrows: "to", dashes: true },
  { from: 1, to: 3, arrows: "to" },
  { from: 1, to: 2, arrows: "to, from" },
  { from: 2, to: 4, arrows: "to, middle" },
  { from: 2, to: 5, arrows: "to, middle, from" },
  { from: 5, to: 6, arrows: { to: { scaleFactor: 2 } } },
  {
    from: 6,
    to: 7,
    arrows: { middle: { scaleFactor: 0.5 }, from: true },
  },
]);

// create a network
var container = document.getElementById("mynetwork");
var data = {
  nodes: nodes,
  edges: edges,
};
var options = {};
var network = new vis.Network(container, data, options);

    </script>
    <script type="text/javascript">
        
var array = [];
var adilist = [
  { id: 99, text: "item 1", date: new Date(2013, 6, 20), group: 1, first: true },
  { id: 92, text: "item 2", date: "2013-06-23", group: 2 },
  { id: 93, text: "item 3", date: "2013-06-25", group: 2 },
  { id: 94, text: "item 4" }];
    
var links = document.getElementsByTagName("a");
for(var i=0, max=links.length; i<max; i++) {
    array.push({id: i, text: "link", date: "2013-06-25", group: 3});
    array.push({id: 23, text: "link", date: "2013-06-25", group: 3});
}
        
nodes.add(adilist
);
              
nodes.add(array
);
        
    </script><!--kg-card-end: html--><!--kg-card-begin: html--><p>
  This example demonstrate using groups. Note that a DataSet is used for both
  items and groups, allowing to dynamically add, update or remove both items and
  groups via the DataSet.
</p>
<div id="visualization"></div>

<!--kg-card-end: html--><p></p><!--kg-card-begin: html--><script>
var now = moment().minutes(0).seconds(0).milliseconds(0);
var groupCount = 3;
var itemCount = 20;

// create a data set with groups
var names = ["John", "Alston", "Lee", "Grant"];
var groups = new vis.DataSet();
for (var g = 0; g < groupCount; g++) {
  groups.add({ id: g, content: names[g] });
}

// create a dataset with items
var items = new vis.DataSet();
for (var i = 0; i < itemCount; i++) {
  var start = now.clone().add(Math.random() * 200, "hours");
  var group = Math.floor(Math.random() * groupCount);
  items.add({
    id: i,
    group: group,
    content:
      "item " +
      i +
      ' <span style="color:#97B0F8;">(' +
      names[group] +
      ")</span>",
    start: start,
    type: "box",
  });
}

// create visualization
var container = document.getElementById("visualization");
var options = {
  groupOrder: "content", // groupOrder can be a property name or a sorting function
};

var timeline = new vis.Timeline(container);
timeline.setOptions(options);
timeline.setGroups(groups);
timeline.setItems(items);


</script><!--kg-card-end: html--><p>1</p><p><a href="__GHOST_URL__/posts">2</a></p><p><a href="__GHOST_URL__/posts/tree-test/123">3</a></p><p>Test</p>
