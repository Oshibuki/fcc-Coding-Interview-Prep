## 数据结构：找到二叉树中的最小高度和最大高度

在上一个挑战中我们提到了树结构不平衡的情况。为了理解平衡的概念，我们来了解一下树的另一个概念：高度（height）。树的高度表示从根节点到叶子结点的距离。如果一个树有很多分支，那么不同的路径（即从根节点到一个子节点的线路）就会有不同的高度。然而，对于一个给定的树，高度一定会有确切的最大值和最小值。如果树是平衡的，最大值和最小值的差值不会超过 1。这意味着在平衡树中，所有的叶子结点都处在同一层级，或者至多只相差一个层级。

树的平衡性这个概念十分重要，因为它直接决定树操作的效率高低。例如在上一节挑战当中，我们提到了不平衡树的最坏情况，此时时间复杂度也会达到最高。自平衡树通常用在拥有动态数据集的树结构当中。常见的平衡树有 AVL 树，红黑树以及 B-trees。当因为插入或删除数据导致这些树结构不平衡时，它们都有内部逻辑处理，让树变得平衡。

注意：深度（depth）是一个与高度类似的概念，它指的是某一个节点（注意，不一定是叶子节点）和根节点之间的距离。

挑战说明：请给二叉树编写两个方法：`findMinHeight`和`findMaxHeight`。这两个方法应该分别返回二叉树的最小高度和最大高度。如果树为空，则两个方法都应返回 -1。最后，为树结构添加`isBalanced`方法，该方法根据树结构是否平衡返回`true`或`false`。你可以使用前两个方法来编写`isBalanced`方法。

```
var displayTree = (tree) => console.log(JSON.stringify(tree, null, 2));
function Node(value) {
    this.value = value;
    this.left = null;
    this.right = null;
}
function BinarySearchTree() {    
    this.root = null;
    // 请把你的代码写在这条注释以下
    this.findMinHeight = function(root=this.root){
      //empty tree
      if(!root){
        return -1
      }
      //leaf node
      if(!root.left && !root.right){
        return 0
      }
      //single child node
      if(!root.left){
        return this.findMinHeight(root.right)+1
      }
      if(!root.right){
        return this.findMinHeight(root.left)+1
      }
      //double child node
      const leftMinHeight = this.findMinHeight(root.left)
      const rightMinHeight = this.findMinHeight(root.right)
      return Math.min(leftMinHeight,rightMinHeight)+1
    }
    this.findMaxHeight = function(root=this.root){
      //empty tree
      if(!root){
        return -1
      }
      //leaf node
      if(!root.left && !root.right){
        return 0
      }
      //single child node
      if(!root.left){
        return this.findMaxHeight(root.right)+1
      }
      if(!root.right){
        return this.findMaxHeight(root.left)+1
      }
      //double child node
      const leftMaxHeight = this.findMaxHeight(root.left)
      const rightMaxHeight = this.findMaxHeight(root.right)
      return Math.max(leftMaxHeight,rightMaxHeight)+1
    }
    this.isBalanced = function(){
      const minHeight = this.findMinHeight()
      const maxHeight = this.findMaxHeight()
      return maxHeight-minHeight <=1
    }
    this.add = function(element){
      let current = this.root
      if(!current){
          this.root = new Node(element)
          return
      }else{
          while (current.value !==element){
              if(element<current.value){
                  if(!current.left){
                      current.left = new Node(element)
                      return
                  }
                  current = current.left
              }else if(element>current.value){
                  if(!current.right){
                      current.right = new Node(element)
                      return
                  }
                  current = current.right
              }
          }
          return null
      }
  }
    // 请把你的代码写在这条注释以上
}

```

