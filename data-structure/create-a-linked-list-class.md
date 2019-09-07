## 数据结构：引入一种新的数据结构：链表

现在我们来创建一个`链表`类。每个链表实例都应该有`head`（表中第一个元素）和`length`（表中元素的个数）这样的基本属性。有些链表会用`tail`属性表示表中最后一个元素，但是本次练习我们只关注 head 和 length 这两个属性。只要我们往链表中添加了元素，`length`属性的数值就会加一。

首先，我们需要创建一个`add`方法，这个方法可以把元素添加进链表。

如果链表为空，那我们只需用`Node`类来创建一个节点，同时让链表的`head`指向该元素即可。

但如果链表中已经存在一些元素，我们该如何添加呢？回想一下，链表中的每个元素都有`next`属性。而且，链表中最后一个节点的`next`是指向`null`的。为了添加新节点，我们首先需要找到链表的最后一个节点，并让该节点的`next`指针指向我们添加的新节点。



------



请写一个`add`方法，当添加第一个元素时让`head`指针指向该元素；之后添加的新元素，前一个节点的`next`属性都应该指向这个新添加的元素。

注意：

每当有新元素添加进链表，`length`的数值都应该加一。

```
function LinkedList() {
    var length = 0;
    var head = null;

    var Node = function(element){
        this.element = element;
        this.next = null;
    };

    this.head = function(){
        return head;
    };

    this.size = function(){
        return length;
    };

    this.add = function(element){
        var node = new Node(element);
        if(head === null){
            head = node;
        } else {
            currentNode = head;
            while(currentNode.next){
                currentNode  = currentNode.next;
            }
            currentNode.next = node;
        }
        length+=1
        // 请把你的代码写在这条注释以上
    };
}
```

