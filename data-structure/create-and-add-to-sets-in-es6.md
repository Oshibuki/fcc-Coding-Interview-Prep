## 数据结构：创建集合并添加项目

在上面的练习中，我们用 ES5 实现了集合，现在我们来用 ES6 实现。在 ES6 中，这些操作会更加简单。我们可以通过 ES6 的内建`Set`数据结构，它也包含了很多上面我们自己写的方法。我们先来一起来看看这些方法：

创建一个空 set：

```
var set = new Set();
```

创建带有一个值的 set：

```
var set = new Set(1);
```

基于数组创建 set：

```
var set = new Set([1, 2, 3]);
```

创建好 set 之后，我们可以通过`add`方法添加元素：

> var set = new Set([1, 2, 3]);
> set.add([4, 5, 6]);

提醒一下，set 数据结构中不允许出现重复元素：

> var set = new Set([1, 2, 3, 1, 2, 3]);
> // set 只包含 [1, 2, 3]



------



请修改`checkSet`函数，让它的返回`1, 2, 3, 'Taco', 'Cat', 'Awesome'`。

```
function checkSet() {
  var set = new Set([1, 2, 3, 3, 2, 1, 2, 3, 1]);
  // 请把你的代码写在这条注释以下
  set.add(['Taco', 'Cat', 'Awesome'])
  // 请把你的代码写在这条注释以上
  console.log(set);
  return set;
}

checkSet();
```

