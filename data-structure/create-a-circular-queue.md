## 数据结构：创建一个循环队列

在本次挑战中我们来创建一个 Circular Queue（循环队列），与普通队列的不同之处在于循环队列的末尾是指向开头的。添加数据时，新元素还是会出现在末尾；但如果队列中的元素已经达到了尽头，则会把新元素添加到开头。这种数据结构在一些特定的场合会比较有用。比如流媒体服务，当队列满了以后新的媒体数据会从头部开始直接覆盖历史数据。

下面我们用数组来举例说明循环队列的概念：

> [1, 2, 3, 4, 5]
> ^Read @ 0
> ^Write @ 0

读和写两个操作都从`0`这个位置开始。现在队列添加了`a`、`b`和`c`3 个数据。新队列如下：

> [a, b, c, 4, 5]
> ^Read @ 0
> ^Write @ 3

读取数据时，我们可以选择移除或者保留数据：

> [null, null, null, 4, 5]
> ^Read @ 3
> ^Write @ 3

一旦写入操作达队列末尾，就会从队列头开始继续写入数据：

> [f, null, null, d, e]
> ^Read @ 3
> ^Write @ 1

虽然这种数据结构有着固定的内存空间，但它可以用于处理占内存较大的文件。

挑战说明：

在本次挑战中我们来实现一个循环队列。该循环队列应该有`enqueue`和`dequeue`这两个方法，我们可以通过这两个方法从队列中读取和写入数据。这个类的构造器应该接收一个整数为参数，因为我们需要通过它来定义队列的长度。我们已经在右边的编辑器中为你写好了这个循环队列的初始版本。循环队列中存在两个指针（在这里，指针就是一个用于表示数组中元素位置的整数），分别是 read pointer（读指针）与 write pointer（写指针），它们分别用于表示数据的开始和结尾。在往循环队列中插入数据时，写指针需要向后移动一个位置，而如果写指针已经到达队列的末尾，则需要回到队列头部继续进行写入操作。类似地，在进行出队操作时，读指针也应该向后移动。写指针的位置不应越过读指针（我们的类当中不允许发生一个数据未经读取就已经被覆盖的情况发生），同时读指针也不应越过已经写入的数据。

此外，`enqueue`方法应该返回成功入队的元素，否则需要返回`null`；类似地，`dequeue`方法应该返回成功出队的元素，否则需要返回`null`。

```javascript
class CircularQueue {
    constructor(size) {

        this.queue = [];
        this.read = 0;
        this.write = 0;
        this.max = size - 1;

        while (size > 0) {
            this.queue.push(null);
            size--;
        }

    }

    print() {
        return this.queue;
    }


    enqueue(item) {
        // 请把你的代码写在这条注释以下
        if(this.queue[this.write] && this.write>=this.read){
            return null
        }else{
            this.queue[this.write] = item
            this.write+=1
            if(this.write>this.max){
                this.write= this.write-(this.max+1)
            }
            return item
        }

        // 请把你的代码写在这条注释以上
    }

    dequeue() {
        // 请把你的代码写在这条注释以下
        if(!this.queue[this.read] && this.read<=this.write){
            return null
        }else{
            let item = this.queue[this.read]
            this.queue[this.read] = null
            this.read++
            if(this.read>this.max){
                this.read= this.read-(this.max+1)
            }
            return item
        }
        // 请把你的代码写在这条注释以上
    }
}
```

