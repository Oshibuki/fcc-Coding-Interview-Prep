## 数据结构：介绍一种新的数据结构：映射（Map）

接下来的几个挑战会涉及到 Map（映射）和 Hash Table（哈希表）这些知识点。Map 是一种存储键值对的数据结构。在 JavaScript 中，对象就是 Map 的一种表现形式。Map 是一种十分通用和高效的数据查询结构，我们可以在 Map 中通过 key（键）快速地获取对应的 value（值）。

挑战说明：现在我们需要创建 Map。鉴于 JavaScript 的对象已经为我们提供了十分高效的 Map 数据结构，我们在本次挑战中写的一些方法只是出于熟悉 Map 的目的。然而 JavaScript 对象本身只为我们提供了少量的操作方法，如果我们想要添加一些自定义方法该怎么办呢？

现在我们使用 JavaScript 对象来模拟`Map`数据结构，我们需要在 Map 对象中创建如下方法：

`add`方法接收`key`和`value`作为参数，并把键值对添加到 Map 中；

`remove`方法接收一个`key`值并移除对应的键值对；

`get`方法接收`key`值，并返回对应的`value`值；

`has`方法根据值的存在情况返回相应的`boolean`值；

`values`方法以数组形式返回 Map 中所有的 value；

`size`方法返回 Map 中元素的个数；

`clear`清空 Map。

```
var Map = function() {
    this.collection = {};
    // 请把你的代码写在这条注释以下
    this.add = function (key,value) {
        this.collection[key] = value
    }
    this.remove = function (key) {
        delete this.collection[key]
    }
    this.get = function (key) {
        return this.collection[key]
    }
    this.has = function (key) {
        return this.collection.hasOwnProperty(key)
    }
    this.values = function () {
        return Object.values(this.collection)
    }
    this.size = function () {
        return Object.keys(this.collection).length
    }
    this.clear = function () {
        this.collection = {}
    }
    // 请把你的代码写在这条注释以上
};

```

