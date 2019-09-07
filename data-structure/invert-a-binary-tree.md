## 数据结构：反转二叉树


这里我们将创建一个反转二叉树的函数。 给定二叉树，我们想要生成一个新树，它等效于该树的镜像。 与原始树的顺序遍历相比，在倒置树上运行中序遍历将以相反的顺序探索节点。 在我们的二叉树上编写一个名为invert的方法。 调用此方法应该反转当前树结构。 理想情况下，我们希望在线性时间内就地执行此操作。 也就是说，我们只访问每个节点一次，我们在不使用任何额外内存的情况下修改现有的树结构。 祝好运！

```
var displayTree = (tree) => console.log(JSON.stringify(tree, null, 2));
function Node(value) {
    this.value = value;
    this.left = null;
    this.right = null;
}
function BinarySearchTree() {
    this.root = null;
    // 请在本行下方输入代码
    this.invert = function(root = this.root) {
      if (!root) {
        return null
      }
      let tmp = root.right
      root.right = root.left
      root.left = tmp

      if (root.left != null) root.left = this.invert(root.left) //递归反转左子节点
      if (root.right != null) root.right = this.invert(root.right) //递归反转右子节点
      return root
    }
    // 请在本行上方输入代码
}
```

