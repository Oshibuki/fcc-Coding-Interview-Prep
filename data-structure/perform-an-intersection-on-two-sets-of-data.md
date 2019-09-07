## 数据结构：求两个集合的交集

在本次练习当中，我们需要在`Set`数据结构中写一个用于计算两集合交集的方法`intersection`。交集的意思是是两个或者多个集合共同拥有的元素组成的集合。该方法应该接收`Set`为参数并返回两个集合的交集。

举个例子，集合`setA = ['a','b','c']`和集合`setB = ['a','b','d','e']`的交集计算结果为：`setA.intersection(setB) = ['a', 'b']`。

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
    // 该方法返回集合长度
    this.size = function() {
        return collection.length;
    };
    // 该方法返回两个集合的交集
    this.union = function(otherSet) {
        var unionSet = new Set();
        var firstSet = this.values();
        var secondSet = otherSet.values();
        firstSet.forEach(function(e){
            unionSet.add(e);
        });
        secondSet.forEach(function(e){
            unionSet.add(e);
        });
        return unionSet;
    };
    // 请把你的代码写在这条注释以下
    this.intersection = function(otherSet){
        var firstSet = this.values();
        var secondSet = otherSet.values();
        var intersectionSet = new Set();
        firstSet.filter(i=>otherSet.has(i)).map(i=>intersectionSet.add(i))
        return intersectionSet
    }
    // 请把你的代码写在这条注释以上
}
```

