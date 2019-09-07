## 数据结构：创建一个双向链表

之前我们创建的都是单向链表，现在我们来创建双向链表。顾名思义，双向链表拥有两个指针，一个指向前一个节点，一个指向后一个节点。

对于这种链表，我们可以从两个方向遍历元素，但因为每个节点都有两个指针，因此这种链表会占据更多的内存空间。



------



在右边的编辑器中，我们已经为你写好了一个`Node`和`DoublyLinkedList`。现在我们来给双向链表添加`add`和`remove`方法。`add`方法应该把指定的元素添加到双向链表中，而`remove`方法应该移除双向链表中的指定元素。

对于双向链表中边界元素的操作，比如移除移除头部或尾部元素时需要谨慎。以及，如果尝试从空链表中移除元素，则应该返回`null`。

```
var Node = function(data, prev) {
    this.data = data;
    this.prev = prev;
    this.next = null;
};
var DoublyLinkedList = function() {
    this.head = null;
    this.tail = null;
    // 请把你的代码写在这条注释以下
    this.add = function(data) {
        if (!this.head) {
            let newNode = new Node(data, null)
            this.head = newNode
            this.tail = newNode
        } else {
            let newNode = new Node(data, this.tail)
            this.tail.next = newNode
            this.tail = newNode
        }
    }
    this.remove =function (data) {
        if(!this.head){
            return null
        }else {
            if(this.head.data === data){
                if(this.tail === this.head ){
                    this.tail = null
                }
                this.head = this.head.next
            }else {
                let currentNode = this.head
                while(currentNode &&currentNode.data !==data){
                    currentNode = currentNode.next
                }
                //循环结束，两种情况：找到对应节点，没找到循环到结尾
                if(currentNode.data === data){
                    if(this.head === currentNode){
                        this.head =  currentNode.next
                        currentNode.next.prev=null
                    }
                    if(this.tail === currentNode){
                        this.tail.prev.next = null
                        this.tail = this.tail.prev
                    }
                    currentNode.prev.next = currentNode.next
                }
            }
        }
    }
    this.print = function () {
        let result = []
        let currentNode = this.head
        while(currentNode){
            result.push(currentNode.data)
            currentNode = currentNode.next
        }
        return result
    }
    // 请把你的代码写在这条注释以上
};

```

