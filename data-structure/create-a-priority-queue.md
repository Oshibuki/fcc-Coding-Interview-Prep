## 数据结构：创建一个优先队列

在这次挑战中我们来创建 Priority Queue（优先队列）。优先队列是一种特殊的队列类型，这种队列中会有额外的信息来说明队列中元素的优先顺序，这种优先顺序可以用整数来表示，元素的优先级会直接影响元素的出队顺序。就算较高优先级的元素比较低优先级的元素后入队，在出队的时候，较高优先级的元素还是会先出队。

举个例子，对于一个拥有 3 个元素的优先队列：

```
[['kitten', 2], ['dog', 2], ['rabbit', 2]]
```

元素中的第二个值（一个整数）代表这个元素的优先级，数字越小则优先级越高。如果我们让优先级为`1`的元素`['human', 1]`入队，那么这个元素在本优先队列中会第一个出队。添加该元素后，新的队列如下：

```
[['human', 1], ['kitten', 2], ['dog', 2], ['rabbit', 2]]
```

我们已经在右侧的代码编辑器中编写了`PriorityQueue`。你需要添加一个`enqueue`方法，使用该方法入队的元素都带有优先级；添加一个移除元素的`dequeue`方法；添加能够返回队列中元素总数的`size`方法；添加能够返回队列头部元素的`front`方法；添加`isEmpty`方法，当队列为空时`isEmpty`方法返回`true`，否则返回`false`。

`enqueue`方法接收类似于`['human', 1]`的元素作为参数，其中数字`1`表示元素优先级。`dequeue`方法应该返回元素内容，无需返回它的优先级。

```
function PriorityQueue () {
    this.collection = [];
    this.printCollection = function() {
      console.log(this.collection);
    };
    // 请把你的代码写在这条注释以下
    this.enqueue = function(item){
        let added =false
        for(let i=0;i<this.collection.length;i++){
            if(item[1]<this.collection[i][1]){
                this.collection.splice(i,0,item)
                added = true
                break
            }
        }
        if(!added){
            this.collection.push(item)
        }
    }
    this.dequeue = function(){
        return this.collection.shift()[0]
    }
    this.size= function(){
        return this.collection.length
    }
    this.isEmpty = function(){
        return this.collection.length===0
    }
    // 请把你的代码写在这条注释以上
}
```

参考链接：https://www.geeksforgeeks.org/implementation-priority-queue-javascript/