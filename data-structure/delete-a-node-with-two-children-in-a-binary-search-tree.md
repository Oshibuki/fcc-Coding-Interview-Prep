## 数据结构：删除二叉树中有两个子节点的节点

移除拥有两个子节点的节点是最难处理的情况，因为移除这种节点会让它的两个子树独立。我们该如何重连这两个子树呢？一种方法是找到需要删除节点的右子树中的最小值，并把这个最小值复制到被删除的那个节点。以这种方式选择的新节点，它的值一定会大于它左子树中所有节点的值；同时这个新节点的值也一定会小于它右子树中所有节点的值。

在复制操作之后，我们还需要把它从右子树移除。需要注意的是，我们现在要删除的这个节点可能是右子树的叶子节点，也可能是这个节点本身还存在子树。如果这个节点是叶子结点，那我们就只须移除其父节点和它的连接。否则，我们就需要让这个节点的父节点指向这个节点的右子树。如果你不明白这个逻辑，请自己尝试画一个图。

挑战说明：现在我们要处理第三种情况以完善`remove`方法。我们已经为你写好了之前两种情况的代码，现在请你来编写删除拥有两个子节点的节点的代码。同时，别忘了考虑极端情况，比如树结构中只有三个节点的情况。解决了这种情况也就意味着我们彻底完成了二叉查找树中的删除操作。这是一个很难的问题，解决它是一个不小的成就。

```
var displayTree = (tree) => console.log(JSON.stringify(tree, null, 2));
function Node(value) {
  this.value = value;
  this.left = null;
  this.right = null;
}

function BinarySearchTree() {
  this.root = null;
  this.remove = function (value,root = this.root) {
    if (root === null) {
      return null;
    }
    var target;
    var parent = null;
    // 找出要删除的节点及其父节点
    (function findValue(node = root) {
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
      if(target === this.root){
        this.root = null
      }
      if (target == root) {
        target=null
        return target
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
      if(target === root){
        root = (target.left===null)?target.right:target.left
      }
      if(target === this.root){
        this.root = root
      }
      else {
        if (parent.left == target) {
          parent.left = (target.left===null)?target.right:target.left;
        } else {
          parent.right = (target.left===null)?target.right:target.left;
        }
      }
      target = null
      return root
    }
    // 情况 3：要删除的节点有两个子节点，请把你的代码写在这条注释以下
    if(children ===2){
      let tmp = this.findMin(target.right)
      target.value = tmp
      target.right = this.remove(tmp,target.right)
    }
  };

  this.findMin = function(root = this.root){
    if(!root){
      return null
    }
    let current = root
    while(current.left){
      current = current.left
    }
    return current.value
  }

  this.depthSearchResult = []
  this.inorder = function(root = this.root) {
    if (!root) {
      return null
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
}
```

