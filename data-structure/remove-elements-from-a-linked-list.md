## 数据结构：从链表中删除元素

链表中一个重要的方法是`remove`。该方法接收一个元素作为参数，然后在链表中找到并移除该元素。

在链表中移除节点并不只是从仅仅删除掉一个元素那么简单。在链表中，每个节点的`next`指针都会指向表中的下一个节点。因此，在移除节点时，我们需要确保这个被移除节点的前一个节点的`next`指针指向被移除节点的下一个节点。

这样解释可能比较抽象，因此我们再来回想一下上面提到的老鹰捉小鸡。想象一下，在扮演鸡仔的队伍中，你正前方的人离开了队伍。这个离队的人也就不再会把手搭在他前一个人的肩上，同时你的手也不可能继续搭在离队的那个人肩上。接下来你需要向前走一步，把你的手搭在他前面的那个人肩上。

如果我们移除的是头部元素，那么我们需要让`head`指针指向链表中的下一个元素（即移除前的第二个元素）。



------



请编写`remove`方法，该方法接收一个元素作为参数并从链表中移除该元素。

注意：

每当有元素从链表中移除，`length`的数值都应该减一。

```
function LinkedList() { 
  var length = 0; 
  var head = null; 

  var Node = function(element){ 
    this.element = element; 
    this.next = null; 
  }; 

  this.size = function(){
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
        let currentNode = head;

        while(currentNode.next){
            currentNode  = currentNode.next;
        }

        currentNode.next = node;
    }

    length++;
  }; 

  this.remove = function(element){
    // 请把你的代码写在这条注释以下
    if(head.element === element){
      head = head.next
    }else{
      let currentNode = head;
      while(currentNode.next){
        if(currentNode.next.element === element){
          currentNode.next = currentNode.next.next
        }
      }
    }
    length -=1
    // 请把你的代码写在这条注释以上
  };
}
```

