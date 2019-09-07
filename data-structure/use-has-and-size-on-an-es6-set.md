## 数据结构：使用集合的 has 和 size 方法

现在我们来学习 ES6 Set 对象的`has`和`size`方法。

首先，创建一个 ES6 Set：

```
var set = new Set([1,2,3]);
```

`has`方法会检查 set 中是否有某个值：

```
var hasTwo = set.has(2);
```

`size`会返回 Set 的长度：

```
var howBig = set.size;
```



------



在本次练习当中我们会给`checkSet`函数传入一个数组和一个值作为参数，该函数需要根据传入的数组参数创建一个 ES6 set，并检查该 set 中是否存在该第二个参数值。这个函数的返回值为一个数组，第一个元素为`true`或`false`，用于表示 set 中是否存在第二个参数值；第二个元素为 set 的长度。

```
function checkSet(arrToBeSet, checkValue){

   // 请把你的代码写在这条注释以下
    let result = new Set(arrToBeSet)
    let checkResult = result.has(checkValue)?true:false
    return [checkResult,result.size]
   // 请把你的代码写在这条注释以上

}

checkSet([ 1, 2, 3], 2); // 应该返回 [ true, 3 ]
```

