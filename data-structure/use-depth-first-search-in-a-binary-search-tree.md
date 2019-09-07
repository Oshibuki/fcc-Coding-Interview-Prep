## 数据结构：在二叉树中使用深度优先搜索

我们已经了解了如何在二叉查找树当中找到一个值。但是如果我们只想遍历整棵树呢？或者我们想在一个乱序的树结构中找到一个值又该如何操作呢？接下来我们就介绍一些树的遍历算法。第一个方法就是深度优先（depth-first）查找方法。在深度优先查找当中，需要先走完（遍历完）当前子树，再去遍历下一个子树。我们有三种方式可以实现深度优先查找：

中序（in-order）：先访问最左端节点，然后访问根节点，最后访问最右端节点。

前序（pre-order）：先访问根节点，然后访问子树。

后序（post-order）：先访问子树，最后访问根节点。

我们应该根据树结构中存储数据的类型以及所要查找的值来选择不同的查找方法。对于二叉查找树，中序遍历会按大小顺序返回所有的节点值。

挑战说明：我们需要为二叉查找树添加这三个查找方法。深度优先查找本身就是一种递归操作，只要当前节点存在子节点，遍历就会一直进行到底。只要你能理解这个基本概念，你就可以调整遍历过程中节点的访问顺序，也就可以写出这三种查找方法。例如，在后序遍历中，我们在访问任何父级节点之前需要递归地遍历完它的所有子节点；然而在前序遍历中，遍历完节点的一个分支之后，我们需要先回到父节点，再递归地遍历它的另一个分支。

在树中定义`inorder`、`preorder`、`postorder`方法。三个方法都应该返回一个数组，该数组用于表示树的遍历结果。每个节点返回的都应该是整数值，而非节点本身。以及，如果树为空，那么三个方法都应该返回`null`。

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

  this.add = function(element) {
    let current = this.root
    if (!current) {
      this.root = new Node(element)
      return
    } else {
      while (current.value !== element) {
        if (element < current.value) {
          if (!current.left) {
            current.left = new Node(element)
            return
          }
          current = current.left
        } else if (element > current.value) {
          if (!current.right) {
            current.right = new Node(element)
            return
          }
          current = current.right
        }
      }
      return null
    }
  }

  this.depthSearchResult = []
  this.inorder = function(root = this.root) {
    if (!root) {
      return
    }
    this.inorder(root.left)
    this.depthSearchResult.push(root.value)
    this.inorder(root.right)
    if(root === this.root){
      let tmp = this.depthSearchResult
      this.depthSearchResult = []
      return tmp
    }
  }

  this.preorder = function(root = this.root) {
    if (!root) {
      return
    }
    this.depthSearchResult.push(root.value)
    this.preorder(root.left)
    this.preorder(root.right)
    if(root === this.root){
      let tmp = this.depthSearchResult
      this.depthSearchResult = []
      return tmp
    }
  }

  this.postorder = function(root = this.root) {
    if (!root) {
      return
    }
    this.postorder(root.left)
    this.postorder(root.right)
    this.depthSearchResult.push(root.value)
    if(root === this.root){
      let tmp = this.depthSearchResult
      this.depthSearchResult = []
      return tmp
    }
  }
  // 请把你的代码写在这条注释以上
}
```

