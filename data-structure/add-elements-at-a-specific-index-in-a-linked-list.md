## 数据结构：在链表的指定索引处添加元素

现在我们来创建一个`addAt(index, element)`方法，该方法在指定的位置添加一个元素。

就像我们移除指定位置的元素一样，在遍历链表时需要及时更新 currentIndex 的数值。当 currentIndex 与给定的 index 值相等时，我们需要让这个节点的前一个节点指向新添加的节点，以及让新添加的节点指向这个节点。

再来回想一下老鹰捉小鸡的例子，有一个新队员想加入扮演鸡仔的队伍的中间位置，而你就在队伍中间。因此你需要将手从前一个人的肩上拿开，而新加入的人则将他的手搭到了你刚才搭的那个人的肩上，最后你需要将你的手搭在新加入队伍的这个人肩上。

挑战说明：

创建一个`addAt(index, element)`方法，该方法可以为链表在指定位置添加元素。如果元素未能成功添加则返回 false。

注意：

记得检查 index 的值是否小于 0 或大于等于链表长度。

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

  // 请把你的代码写在这条注释以下
  this.addAt = function(index,element){
    let newNode = new Node(element)
    if(index<0){
      return false
    }else if(index===0){
      newNode.next = head
      head=newNode
      length+=1
    }else if(index>=length){
      return false
    }else{
      let currentIndex=0
      let currentNode= head
      while(currentIndex<index-1){
        currentNode = currentNode.next
      }
      newNode.next =  currentNode.next
      currentNode.next = newNode
      length+=1
    }
  }
  // 请把你的代码写在这条注释以上

}
```

