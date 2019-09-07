## 数据结构：删除二叉树中有一个子节点的节点

现在我们已经知道如何删除一个叶子结点了。在这个挑战中，我们来接着尝试删除有一个子节点的节点。比如，对于一个结构为 1 - 2 - 3 的树，它有三个节点：其中 1 是根节点。现在如果我们要删除节点 2，那直接让节点 1 指向节点 3 即可。通常，删除只有一个子节点的节点时，我们只需要让该节点的父节点指向该节点的子节点即可。

挑战说明：我们已经在右边为你写好了`remove`方法，其中还包含了上一个挑战的实现。与之前的题目描述一样，我们找到需要删除的节点以及其父节点，然后用定义好的方法判断出该节点拥有的子节点数量。现在我们来处理删除仅有一个子节点的节点的情况。首先，我们需要知道这一个子节点是左分支还是右分支，然后才能让被删除节点的父节点的合适分支来指向该节点的子节点。此外，我们需要考虑当删除的节点为根节点的情况，这意味着父节点的值是`null`。当然，如果你觉得提供给你的代码不够好，也可以用你自己写的版本。

```
var displayTree = (tree) => console.log(JSON.stringify(tree, null, 2));
function Node(value) {
  this.value = value;
  this.left = null;
  this.right = null;
}

function BinarySearchTree() {
  this.root = null;
  this.remove = function(value) {
    if (this.root === null) {
      return null;
    }
    var target;
    var parent = null;
    // 找出要删除的节点及其父节点
    (function findValue(node = this.root) {
      if (value == node.value) {
        target = node;
      } else if (value < node.value && node.left !== null) {
        parent = node;
        return findValue(node.left);
      } else if (value < node.value && node.left === null) {
        return null;
      } else if (value > node.value && node.right !== null) {
        parent = node;
        return findValue(node.right);
      } else {
        return null;
      }
    }).bind(this)();
    if (target === null) {
      return null;
    }
    // 获取要删除节点的子节点数量
    var children = (target.left !== null ? 1 : 0) + (target.right !== null ? 1 : 0);
    // 情况 1：要删除的节点没有子节点
    if (children === 0) {
      if (target == this.root) {
        this.root = null;
      }
      else {
        if (parent.left == target) {
          parent.left = null;
        } else {
          parent.right = null;
        }
      }
    }
    // 情况 2：要删除的节点只有一个子节点，请把你的代码写在这条注释以下
    if(children ===1){
      if(target === this.root){
        this.root = (target.left===null)?target.right:target.left
      }
      else {
        if (parent.left == target) {
          parent.left = (target.left===null)?target.right:target.left;
        } else {
          parent.right = (target.left===null)?target.right:target.left;
        }
      }
    }
  };
}
```

