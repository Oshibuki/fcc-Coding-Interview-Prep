## 数据结构：介绍一种新的数据结构：集合（Set）

在接下来的几个章节里面我们会通过创建一个函数来模拟 "Set"（集合）数据结构。集合跟数组很类似，但是集合中元素具有唯一性。集合的典型应用是检查其中是否存在某个数据。在 JavaScript 中，我们可以通过对象实现，举例如下：

> var set = new Object();
> set.foo = true;
> // 检查 foo 是否存在：
> console.log(set.foo) // 输出 true

在接下来的几个练习中，我们会从零开始创建一个拥有完整功能的集合。

在本次练习中，你需要创建一个`add`方法。它的作用是添加集合中不存的元素：

> this.add = function(element) {
> // 将元素添加进集合的代码
> }

如果元素成功添加进集合，`add`方法应返回`true`，否则应返回`false`。



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
    // 请把你的代码写在这条注释以下
    this.add = function(element){
        if(this.has(element)){
            return false
        }else{
            collection.push(element)
            return true
        }
    }
    // 请把你的代码写在这条注释以上
}
```

