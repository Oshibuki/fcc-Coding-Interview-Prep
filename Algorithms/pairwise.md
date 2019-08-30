## 算法：结对

给定一个数组`arr`，查找其总和等于第二个参数“`arg `”的元素对，并返回其索引的总和。

你可以使用多个具有相同数字元素但不同索引的对。每对应该使用尽可能低的可用索引。一旦一个元素被使用，它就不能被重用来与另一个元素配对。例如，`pairwise([1, 1, 2], 3)`使用索引为 0 的元素 1 而不是索引为 1 的元素 1 创建一对`[ 2，1 ]`，因为 0 + 2 < 1 + 2。

例如：`pairwise([7, 9, 11, 13, 15], 20)`返回`6`。满足和为 20 的一组数组是：`[7, 13]`和`[9, 11]`，然后我们可以写出对应的数组，以及他们的索引与他们的值。

| **索引** | 0    | 1    | 2    | 3    | 4    |
| :------- | :--- | :--- | :--- | :--- | :--- |
| 值       | 7    | 9    | 11   | 13   | 15   |

然后我们将对应的索引相加，

7 + 13 = 20 →；索引 0 + 3 = 3
9 + 11 = 20 →； 索引 1 + 2 = 3
3 + 3 = 6 → 应该返回`6`。



```javascript
function pairwise(arr, arg) {
    let isUsed = new Array(arr.length).fill(false)

    for (let i = 0; i < arr.length; i++) {
        for (let j = i+1; j < arr.length; j++) {
            if (!isUsed[i] && !isUsed[j]) {
                if (arr[i] + arr[j] === arg) {
                    isUsed[i] = true
                    isUsed[j] = true
                }
            }
        }
    }

    return arr.reduce(function (accum,current,index,arr) {
        if(isUsed[index]){
          return  accum+index
        }else {
         return   accum
        }
    },0)
}

pairwise([1,4,2,3,0,5], 7);
```

