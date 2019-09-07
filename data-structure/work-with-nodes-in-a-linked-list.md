## 数据结构：使用链表中的节点

计算机科学中，另一个比较常见的数据结构是链表。链表是一系列数据元素的线性集合，每个元素称为节点（nodes）；且每个节点都有指向下一个节点的指针。因此，链表中的每个节点由元素本身和指向下一个节点的引用组成。

这种数据结构可以类比老鹰捉小鸡的游戏，游戏中所有扮演鸡仔的人需要躲在母鸡身后，手要搭在前一个人的肩上。你可以看到你前面的人是谁，但是看不到再前面的人。一个节点就如同一个扮演鸡仔中的一个人：这个人知道自己是谁，也只能看到前面的一个人，但他无法看到其他人。



------



在代码编辑器中，我们已经创建了`Kitten`和`Puppy`两个节点，而且我们已经将`Kitten`节点和`Puppy`节点连接起来。

请创建`Cat`和`Dog`两个节点，并把他们添加到`Kitten`和`Puppy`之后。

```
var Node = function(element){
    this.element = element; 
    this.next = null; 
};
var Kitten = new Node("Kitten");
var Puppy = new Node("Puppy");

Kitten.next = Puppy;
// 请把你的代码写在这条注释以下
var Cat = new Node("Cat");
var Dog = new Node("Dog");
Puppy.next = Cat;
Cat.next= Dog
// 你可以修改这行代码来进行测试
console.log(Kitten.next);
```

