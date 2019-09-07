## 数据结构：求两个集合的差异

在本次练习中，我们需要在`Set`数据结构中创建一个计算两集合差集的`difference`方法。两个集合差集的概念为：由第一个集合中存在且第二个集合中不存在的元素组成的集合。该方法应该接收另一个`Set`作为参数并且返回两个集合的差集。

举个例子，集合`setA = ['a','b','c']`与`setB = ['a','b','d','e']`的差集比较结果为：`setA.difference(setB) = ['c']`。

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
    // 该方法会返回两个集合的交集
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
    // 该方法会返回两个集合的差集
    this.intersection = function(otherSet) {
        var intersectionSet = new Set();
        var firstSet = this.values();
        firstSet.forEach(function(e){
            if(otherSet.has(e)){
                intersectionSet.add(e);
            }
        });
        return intersectionSet;
    };
    // 请把你的代码写在这条注释以下
    this.difference = function(otherSet){
        var differenceSet = new Set();
        var firstSet = this.values();
        firstSet.map(i =>{
            if(!otherSet.has(i)){
                differenceSet.add(i)
            }
        })
        return differenceSet

    }
    // 请把你的代码写在这条注释以上
}
```

