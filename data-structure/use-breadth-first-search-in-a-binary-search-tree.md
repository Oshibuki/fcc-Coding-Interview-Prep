## 数据结构：在二叉树中使用广度优先搜索

现在我们来介绍另一种树结构遍历方法：广度优先（breadth-first）查找。相较于前一节挑战中的深度优先查找方法，在访问下一层之前，广度优先查找方法会先遍历完上一层。通常，广度优先查找算法可以通过队列（queue）来实现。

这种遍历方式的核心思路是发生在根节点入队后的一个循环：首先我们让队列头元素出队并把该出队元素添加到结果中。之后，我们检查这个出队的元素对应的节点是否有子节点。如果有，就把它的子节点都添加到队列。然后，回到开头的出队并添加到结果这一操作。这个过程一直持续到队列为空。因此，一开始我们需要先让树的根节点入队，这样队列才有头元素可以出队。

挑战说明：请为树结构添加一个名为`levelOrder`的广度优先查找方法。该方法应该通过广度优先查找方式遍历树中的所有数据值。我们需要确保数组中的元素是节点的数值而非节点本身。对于同一层级，子节点应从左至右的顺序遍历。然后，我们再来写一个叫做`reverseLevelOrder`的方法，该方法以从右至左的顺序遍历同一层级的子节点。

```
var displayTree = tree => console.log(JSON.stringify(tree, null, 2))
function Node(value) {
  this.value = value
  this.left = null
  this.right = null
}
function BinarySearchTree() {
  this.root = null
  // 请把你的代码写在这条注释以下
  this.levelOrder= function(root = this.root){
    if(!root){
      return null
    }
    let nodeQueue = [],result = []
    nodeQueue.push(root)
    while(nodeQueue.length>0){
      let current = nodeQueue.shift()
      result.push(current.value)
      if(current.left){
        nodeQueue.push(current.left)
      }
      if(current.right){
        nodeQueue.push(current.right)
      }
    }
    return result
  }

  this.reverseLevelOrder = function(root = this.root){
      if(!root){
        return null
      }
      let nodeQueue = [],result = []
      nodeQueue.push(root)
      while(nodeQueue.length>0){
        let current = nodeQueue.shift()
        result.push(current.value)
        if(current.right){
          nodeQueue.push(current.right)
        }
        if(current.left){
          nodeQueue.push(current.left)
        }
      }
      return result
    }
  // 请把你的代码写在这条注释以上
}
```

