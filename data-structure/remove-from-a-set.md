## 数据结构：从集合中移除

在本次练习当中我们来为集合创建一个删除方法，该方法命名为`this.remove`。它接收一个值并判断该值在集合中是否存在，如何存在就从集合中移除该元素并返回`true`，否则返回`false`。

```
function Set() {
    // collection 变量用来存储集合中的元素
    var collection = [];
    // 当集合中存在 element 元素时返回 true 否则返回 false 
    this.has = function(element) {
        return (collection.indexOf(element) !== -1);
    };
    // 该方法会返回集合内所有元素
    this.values = function() {
        return collection;
    };
    // 该方法会把 element 添加到集合中
    this.add = function(element) {
        if(!this.has(element)){
            collection.push(element);
            return true;
        }
        return false;
    };
    // 请把你的代码写在这条注释以下
    this.remove = function(element){
        if(!this.has(element)){
            return false;
        }
        let index = collection.indexOf(element)
        collection.splice(index,1)
        return true
    }
    // 请把你的代码写在这条注释以上
}
```

