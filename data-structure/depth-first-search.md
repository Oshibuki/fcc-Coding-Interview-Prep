## 数据结构：深度优先搜索

与广度优先搜索类似，这里我们将学习另一种称为深度优先搜索的图遍历算法。

广度优先搜索搜索远离源节点的增量边长度，而深度优先搜索首先尽可能地沿着边缘路径向下搜索 。

一旦到达路径的一端，搜索将回溯到具有未访问边路径的最后一个节点并继续搜索。

在视觉上，这就是算法正在做的事情，其中顶部节点是搜索的起始点。

[![img](https://camo.githubusercontent.com/aaad9e39961daf34d967c616edeb50abf3bf1235/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f372f37662f44657074682d46697273742d5365617263682e676966)](https://camo.githubusercontent.com/aaad9e39961daf34d967c616edeb50abf3bf1235/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f372f37662f44657074682d46697273742d5365617263682e676966)

该算法的简单输出是可从给定节点到达的节点列表。因此，在实施此算法时，您需要跟踪您访问的节点。

## Instructions

编写一个函数dfs（），它接受一个无向，邻接矩阵graph和一个节点标签root参数。节点标签将只是0和n  -  1之间节点的数值，其中n是图中节点的总数。

您的函数应输出从root可到达的所有节点的数组。

```
function dfs(graph, root) {
  var stack = [];
  var tempV;
  var visited = [];

  stack.push(root);
  
  while (stack.length > 0) {
    tempV = stack.pop()
    if (visited.indexOf(tempV) == -1) {
      visited.push(tempV);
      let tempVNeighbors = graph[tempV];
      for (var i = 0; i < tempVNeighbors.length; i++) {
        if (tempVNeighbors[i] == 1) {
          stack.push(i);
        }
      }
    }
 }

  return visited;
};


var exDFSGraph = [
  [0, 1, 0, 0],
  [1, 0, 1, 0],
  [0, 1, 0, 1],
  [0, 0, 1, 0]
];
console.log(dfs(exDFSGraph, 3));
```

