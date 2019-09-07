##  数据结构：集合的大小

在本次练习中，我们需要为集合创建一个`size`方法，该方法名为`this.size`，调用该方法时会返回集合的长度。

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
    // 该方法用于从集合中移除 element 元素
    this.remove = function(element) {
        if(this.has(element)){
           var index = collection.indexOf(element);
            collection.splice(index,1);
            return true;
        }
        return false;
    };
    // 请把你的代码写在这条注释以下
    this.size = function(){
        return collection.length
    }
    // 请把你的代码写在这条注释以上
}
```

