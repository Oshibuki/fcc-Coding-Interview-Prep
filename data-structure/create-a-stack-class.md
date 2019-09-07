## 数据结构：创建一个栈

在上一节，我们讨论了什么是栈以及如何用数组来表示栈。在本节，我们将构造自己的栈。

虽然我们可以使用数组来表示栈，但如果我们可以更完备地定义栈拥有的方法，就可以在开发中更好地使用它。

除了`push`和`pop`两个方法，栈还应有一些其他方法。现在我们来给栈添加`peek`、`isEmpty`以及`clear`方法。

挑战说明：

请编写能够将元素压入栈顶的`push`方法、移除栈顶元素的`pop`方法、查看栈中第一个元素的`peek`方法、判断栈是否为空的`isEmpty`方法、以及清空栈内所有元素的`clear`方法。

顺便，我们在右侧代码区为栈添加了一个`print`方法，该方法会打印出集合。不过一般来说，栈是没有这个方法的。

```
function Stack() { 
    var collection = [];
    this.print = function() {
        console.log(collection);
    };
    // 请把你的代码写在这条注释以下
    this.push = function(item){
        collection.push(item)
    }
    this.pop = function(){
        return collection.pop()
    }
    this.peek = function(){
        return collection[collection.length-1]
    }
    this.isEmpty = ()=>{
        return collection.length===0
    }
    this.clear=function(){
        collection = []
    }

    // 请把你的代码写在这条注释以上
}
```

