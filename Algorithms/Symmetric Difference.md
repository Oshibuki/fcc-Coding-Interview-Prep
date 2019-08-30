## 算法：找到对等分差

知识提要：[对称差 (Symmetric Difference)](https://baike.baidu.com/item/对称差)，数学上，两个[集合](https://baike.baidu.com/item/集合/2908117)的对称差分是只属于其中一个集合，而不属于另一个集合的元素组成的集合，例如：集合`let A = [ 1, 2, 3]`和`let B = [ 2, 3, 4]`的对称差分为`A △ B = C = [ 1, 4]`。 集合论中的这个运算相当于布尔逻辑中的异或运算。

创建一个函数 sym，输入两个或两个以上的数组作为参数，然后返回值为*对称差分*的数组

思路：设定两个数组 (例如：`let A = [1, 2, 3]`，`let B = [2, 3, 4]`)作为参数传入，返回对称差分数组（`A △ B = C = [1, 4]`），且数组中没有重复项。

```javascript
function sym(arg) {
    var argArr = [].slice.call(arguments);

    return argArr.reduce(function(accum, e) {
        return accum.concat(e).filter(function(ele) {
            return accum.indexOf(ele) === -1 || e.indexOf(ele) === -1
        }).filter(function(e, i, arr) {
            return arr.indexOf(e) === i;
        });
    });
}
```

