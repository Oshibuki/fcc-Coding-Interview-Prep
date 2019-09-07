## 数据结构：将新元素添加到二叉树中

相信你现在已经对二叉树有了基本的了解，我们来试着写一个稍复杂的方法。

在本次挑战中，我们需要创建一个方法`add`，该方法可以把新节点添加到二叉查找树中。注意二叉查找树的原则：左子树上的数值应该小于等于父节点数值，而右子树上的数值应该大于等于父节点数值。同时，我们应保证树中的所有数值唯一，即不存在重复值。如果试图往树中添加已经存在的值，add 方法应该返回`null`。反之，如果成功添加元素，add 方法应返回`undefined`。

提示：树天然就是一种递归型的数据结构！



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

