## 数据结构：邻接表

图表可以以不同方式表示。这里我们描述一种方法，称为邻接列表 。邻接列表本质上是项目符号列表，其中左侧是节点，右侧列出它所连接的所有其他节点。下面是邻接列表的表示。

> Node1：Node2，Node3
> Node2：Node1
> Node3：Node1

以上是无向图，因为`Node1``Node2``Node3``Node2``Node3``Node2: Node1``Node2``Node1`

> var undirectedG = {
> Node1：[“Node2”，“Node3”]，
> Node2：[“Node1”]，
> Node3：[“Node1”]
> };

这也可以更简单地表示为一个数组，其中节点只有数字而不是字符串标签。

> var undirectedGArr = [
> [1,2]，＃Node1
> [0]，＃Node2
> [0] #Node3
> ]。

## Instructions

创建一个社交网络作为无向图，其中有4个节点/人名为`James``Jill``Jenny``Jeff`

```
var undirectedAdjList = {
    James: ["Jeff"],
    Jill: ["Jenny"],
    Jenny: ["Jill", "Jeff"],
    Jeff: ["Jenny", "James"]
};
```

