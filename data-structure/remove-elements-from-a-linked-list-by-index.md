## 数据结构：在链表中按索引删除元素

在学习其他数据结构之前，我们再来做两个与链表相关的练习。

首先，我们来写一个`removeAt`方法，该方法根据给定的`index`删除对应位置上的`element`。我们把这个方法命名为`removeAt(index)`。为了移除给定位置上的`element`，我们需要用一个变量（也可以叫指针）来记录我们遍历到的位置。

在遍历链表中元素时，我们通常需要一个指向代码中当前遍历到的元素的指针。在本例中，我们从表的头部开始，设置`currentIndex`的初始值为`0`。每 “经过” 一个元素，我们都需要让`currentIndex`加一。

就像`remove(element)`方法一样，删除的时候不仅仅是移除元素那么简单，我们需要保证被移除节点的前一个节点的`next`指针指向被移除节点的下一个节点。



------



请编写`removeAt(index)`方法，移除指定位置的节点，同时该方法需要返回被移除的节点。如果`index`的值为负数或者大于等于链表的长度，该方法应该返回`null`。

注意：

记得及时更新`currentIndex`的数值。

```
function LinkedList() {
    var length = 0;
    var head = null;

    var Node = function (element) { // {1}
        this.element = element;
        this.next = null;
    };

    this.size = function () {
        return length;
    };

    this.head = function () {
        return head;
    };

    this.add = function (element) {
        var node = new Node(element);
        if (head === null) {
            head = node;
        } else {
            let currentNode = head;

            while (currentNode.next) {
                currentNode = currentNode.next;
            }

            currentNode.next = node;
        }

        length++;
    };

    this.remove = function (element) {
        var currentNode = head;
        var previousNode;
        if (currentNode.element === element) {
            head = currentNode.next;
        } else {
            while (currentNode.element !== element) {
                previousNode = currentNode;
                currentNode = currentNode.next;
            }

            previousNode.next = currentNode.next;
        }

        length--;
    };

    // 请把你的代码写在这条注释以下
    this.indexOf = function (element) {
        let currentNode = head;
        for (let i = 0; i < length; i++) {
            if (currentNode && currentNode.element === element) {
                return i
            } else {
                currentNode = currentNode.next
            }
        }
        return -1
    }
    this.elementAt = function (index) {
        let currentNode = head;
        let currentIndex = 0
        while (currentIndex < index) {
            currentNode = currentNode.next
            currentIndex++
        }
        return currentNode.element
    }
    this.removeAt = function (index) {
        if (index < 0 || index >= length) {
            return null
        } else {
            let currentNode = head;
            let currentIndex = 0
            while (currentIndex < index - 1) {
                currentNode = currentNode.next
                currentIndex++
            } //get target node's previous node
            let targetNode = currentNode.next
            currentNode.next = targetNode.next
            length -= 1
            return targetNode.element
        }
    }
    // 请把你的代码写在这条注释以上
}
```

