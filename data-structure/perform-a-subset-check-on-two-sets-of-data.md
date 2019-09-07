## 数据结构：求某个集合是否为另一个集合的子集

在本次练习中我们将对两个集合元素做子集测试。我们会为`Set`数据结构创建`subset`方法。第一个集合会与第二个集合做对比，如果第二个集合完全包含第一个集合内的所有元素，则该方法返回 true 。

举个例子，假设有集合`setA = ['a','b']`与`setB = ['a','b','c','d']`，那么`setA.subset(setB)`的运算结果应该为`true`。

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
    // 该方法会返回两个集合的交集
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
    // 该方法会返回两个集合的差集
    this.difference = function(otherSet) {
        var differenceSet = new Set();
        var firstSet = this.values();
        firstSet.forEach(function(e){
            if(!otherSet.has(e)){
                differenceSet.add(e);
            }
        });
        return differenceSet;
    };
    // 请把你的代码写在这条注释以下
    this.subset = function(otherSet){
        var firstSet = this.values();
        firstSet.every(i => otherSet.has(i))
    }
    // 请把你的代码写在这条注释以上
}
```

