## 数据结构：检查二叉树中是否存在某个元素

现在我们来进一步学习二叉树。对于查找、插入和删除这些操作，二叉查找树的平均时间复杂度是对数级的，这一点我们已经在前面的挑战中提到了。然而极端的情况下，它也可以消耗线性级的时间。

那么极端的情况是什么样子的呢？试想一个由`10`、`12`、`17`、`25`这些值组成的二叉查找树。根据二叉查找树的定义，`12`会添加到`10`的右边，`17`会添加到`12`的右边，而`25`也会添加到`17`的右边，现在我们的树结构就像链表一样。那么，为了找到`25`这个值，我们就需要遍历完所有的元素，这就是最坏的情况。问题的症结在于该树结构是不平衡的。我们会在接下来的挑战逐步说明这意味着什么。

挑战说明：在本次挑战中，我们来为二叉查找树添加一个功能。请编写一个`isPresent`方法，该方法接收一个整数为参数，并返回一个布尔值，用来表示这个数值是否在该二叉查找树中存在。

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
    this.isPresent = function(element){
      if(!this.root){
        return false
      }
      let current = this.root
      while(current && current.value !==element){
        if(current.value>element){
          current = current.left
        }else{
          current = current.right
        }
      }
      if(current && current.value===element){
        return true
      }else{
        return false
      }
    }
    // 请把你的代码写在这条注释以上
}
```

