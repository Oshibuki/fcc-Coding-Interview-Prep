## 数据结构：创建一个队列

如同栈一样，队列也是一系列元素的集合。但是与栈不同的是队列遵循 FIFO（First-In First-Out，先进先出）原则。新增元素会被添加进队列尾部，删除元素则是删除队列头部的元素。

我们可以使用数组像创建栈那样来创建队列，同时我们也希望控制队列拥有哪些操作方法。

`enqueue`和`dequeue`是队列中两个最主要的方法。`enqueue`方法将元素添加至队尾，而`dequeue`方法将队首元素移除并返回该元素。其它比较实用的方法有`front`、`size`和`isEmpty`等。

挑战说明：

请编写`enqueue`方法，该方法将新元素推入队尾；编写`dequeue`方法，该方法移除并返回队首元素；编写`front`方法，该方法返回队首元素；编写`size`方法，该方法返回队列长度；编写`isEmpty`方法，该方法判断队列是否为空。

```
function Queue () { 
    var collection = [];
    this.print = function() {
        console.log(collection);
    };
    // 请把你的代码写在这条注释以下
    this.enqueue = function(item){
        collection.push(item)
    }
    this.dequeue = function(){
       return collection.shift()
    }
    this.front = function(){
        return collection[0]
    }
    this.size = ()=>{
        return collection.length
    }
    this.isEmpty = function(){
        return collection.length===0
    }
    // 请把你的代码写在这条注释以上
}
```

