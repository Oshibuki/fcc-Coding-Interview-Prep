## 数据结构：反转双向链表

现在我们来为双向链表创建一个`reverse`方法，该方法可以反转链表中的元素。在该方法执行后，head 指针应该指向链表尾部，tail 指针则应指向链表头部。此时，如果我们从头到尾遍历链表，则新的链表中节点顺序应与原链表中节点顺序相反。当试图反转一个空链表时，该方法应该返回 null。

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
    
    this.reverse = function () {
        let datas = []
        if(!this.head){
            return null
        }
        let currentNode = this.head
        while(currentNode){
            datas.push(currentNode.data)
            currentNode = currentNode.next
        }
        this.head = null,this.tail = null
        while(datas.length){
            this.add(datas.pop())
        }
    }
    // 请把你的代码写在这条注释以上
};

```

