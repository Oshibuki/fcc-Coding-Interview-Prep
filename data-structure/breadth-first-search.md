## 数据结构：广度优先搜索

到目前为止，我们已经学会了创建图表表示的不同方法。现在怎么办？一个自然的问题是图中任何两个节点之间的距离是多少？进入图遍历算法部分 。 

遍历算法是遍历或访问图中节点的算法。一种遍历算法是**广度优先搜索算法**。

该算法从一个节点开始，首先访问一个边的所有邻居点，然后继续访问邻居点的每个邻居点。

直观的，这就是算法正在做的事情。

[![img](https://camo.githubusercontent.com/2f57e6239884a1a03402912f13c49555dec76d06/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f342f34362f416e696d617465645f4246532e676966)](https://camo.githubusercontent.com/2f57e6239884a1a03402912f13c49555dec76d06/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f342f34362f416e696d617465645f4246532e676966)

要实现此算法，您需要输入图形结构和要启动的节点。

首先，您需要了解距起始节点的距离。这个你想要开始你所有的距离最初一些大的数字，如`Infinity`。这为从起始节点无法访问节点的情况提供了参考。

接下来，您将要从起始节点转到其邻居。 这些邻居是一个边缘，此时你应该添加一个距离单位到你要跟踪的距离。

最后，有助于实现广度优先搜索算法的重要数据结构是队列。 这是一个数组，您可以在其中添加元素到一端并从另一端删除元素。 这也称为FIFO或先进先出数据结构。

------

## Instructions

编写一个函数bfs（），它将邻接矩阵图（二维数组）和节点标签根作为参数。 节点标签将只是0和n-1之间节点的整数值，其中n是图中节点的总数。

您的函数将输出一个JavaScript对象键值对与节点及其与根的距离。 如果无法到达节点，则其距离应为无穷大。

```
function bfs(graph, root) {
  // Distance object returned
  var nodesLen = {};
  
  // Set all distances to infinity
  for (var i = 0; i < graph.length; i++) {
    nodesLen[i] = Infinity;
  }
  nodesLen[root] = 0; // ...except root node
  
  var queue = [root]; // Keep track of nodes to visit
  var current; // Current node traversing

  // Keep on going until no more nodes to traverse
  while (queue.length != 0) {
    current = queue.shift();
    
    // Get adjacent nodes from current node
    var curConnected = graph[current]; // Get layer of edges from current
    var neighborIdx = []; // List of nodes with edges
    var idx = curConnected.indexOf(1); // Get first edge connection
    while (idx != -1) {
      neighborIdx.push(idx); // Add to list of neighbors
      idx = curConnected.indexOf(1, idx + 1); // Keep on searching
    }
    
    // Loop through neighbors and get lengths
    for (var j = 0; j < neighborIdx.length; j++) {
      // Increment distance for nodes traversed
      if (nodesLen[neighborIdx[j]] == Infinity) {
        nodesLen[neighborIdx[j]] = nodesLen[current] + 1;
        queue.push(neighborIdx[j]); // Add new neighbors to queue
      }
    }
  }
  return nodesLen;
};
```

