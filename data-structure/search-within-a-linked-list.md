## 数据结构：在链表中搜索

现在我们来为链表添加一些更加实用的方法。例如我们可以加一个判断链表是否为空的方法，就像之前我们给`Stack`和`Queue`添加的一样。

我们还应该有一个在链表中找某一个具体的元素的方法。对于任何一种数据结构，你都应该在学习时了解它们的遍历方式。现在我们来创建一个`indexOf`方法，该方法接收一个`element`作为参数并返回该元素在链表中的索引值。如果该元素不存在就返回`-1`。

除此之外，我们再来写一个实现相反功能的方法：`elementAt`，该方法接收一个`index`为参数，返回对应位置的`element`。如果`element`没找到就返回`undefined`。



------



请编写`isEmpty`方法来判断链表是否为空，`indexOf`方法返回给定元素的`index`，`elementAt`方法返回给定位置的`element`值。

```
function LinkedList() {
    var length = 0;
    var head = null;

    var Node = function(element){ // {1} 
        this.element = element;
        this.next = null;
    };

    this.size = function() {
        return length;
    };

    this.head = function(){
        return head;
    };

    this.add = function(element){
        var node = new Node(element);
        if(head === null){
            head = node;
        } else {
            var currentNode = head;

            while(currentNode.next){
                currentNode  = currentNode.next;
            }

            currentNode.next = node;
        }

        length++;
    };

    this.remove = function(element){
        var current = head;
        var previousNode;
        if(current.element === element){
            head = current.next;
        } else {
            while(current.element !== element) {
                previousNode = current;
                current = current.next;
            }

            previousNode.next = current.next;
        }

        length --;
    };

    // 请把你的代码写在这条注释以下
    this.indexOf=function(element){
        var current = head;
        for (let i = 0; i < length; i++) {
            if(current && current.element === element){
                return i
            }else{
                current = current.next
            }
        }
        return -1
    }
    this.elementAt = function (index) {
        var current = head;
        var currentIndex = 0
        while (currentIndex<index){
            current = current.next
            currentIndex++
        }
        return current.element
    }
    // 请把你的代码写在这条注释以上
}
```

