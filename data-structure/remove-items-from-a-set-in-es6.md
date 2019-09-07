## 数据结构：移除集合中的项目

现在让我们使用`delete`方法从 ES6 Set 中移除元素。

首先，创建一个 ES6 Set：

```
var set = new Set([1,2,3]);
```

使用`delete`方法从 Set 中移除一个元素：

> set.delete(1);
>
> console.log([...set]) // 输出 [ 2, 3 ]
>
> 

------



请修改`checkSet`函数，先创建一个包含 1、2、3、4、5 这些整数的 set，然后移除元素 2 和 5，并返回移除元素后的 set。

```
function checkSet(){
   var set = new Set([1,2,3,4,5]) // 创建包含 1、2、3、4、5 这 5 个整数的 set
   set.delete(2)// 移除 2
   set.delete(5)// 移除 5
   // 返回 set
   return set;
}
```

