## 数据结构：求两个集合的并集

在本次练习中，我们来写一个合并两个集合中元素的方法。我们需要在`Set`数据结构中创建`union`方法，该方法接收另一个`Set`为参数并返回两个集合中，非重复元素的合集。

举个例子，集合`setA = ['a','b','c']`和集合`setB = ['a','b','d','e']`合并之后的集合为：`setA.union(setB) = ['a', 'b', 'c', 'd', 'e']`。

```
function Set() {
    // collection 变量用来存储集合中的元素
    var collection = [];
    // 当集合中存在 element 元素时返回 true 否则返回 false
    this.has = function (element) {
        return (collection.indexOf(element) !== -1);
    };
    // 该方法会返回集合内所有元素
    this.values = function () {
        return collection;
    };
    // 该方法会把 element 添加到集合中
    this.add = function (element) {
        if (!this.has(element)) {
            collection.push(element);
            return true;
        }
        return false;
    };
    // 该方法用于从集合中移除 element 元素
    this.remove = function (element) {
        if (this.has(element)) {
            var index = collection.indexOf(element);
            collection.splice(index, 1);
            return true;
        }
        return false;
    };
    // 该方法返回集合长度
    this.size = function () {
        return collection.length;
    };
    // 请把你的代码写在这条注释以下
    this.union = function (set) {
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
    }
    // 请把你的代码写在这条注释以上
}

var setA = new Set();
var setB = new Set();
setA.add("a");
setA.add("b");
setA.add("c");
setB.add("c");
setB.add("d");
var unionSetAB = setA.union(setB);
var final = unionSetAB.values();
console.log(final.indexOf("a") !== -1)
console.log(final.indexOf("b") !== -1)
console.log(final.indexOf("c") !== -1)
console.log(final.indexOf("d") !== -1)
console.log(final.length === 4)
```

