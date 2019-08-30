## 算法：插入排序

现在我们开始研究[插入排序](https://baike.baidu.com/item/插入排序)。这个方法通过在列表的开头见一个排序的数组来实现整个排序，它以第一个元素开始排序数组，然后检查对比下一个元素，并将其向后交换到排序的书中，直到它处在排序的位置。循环迭代整个列表，将新产生的元素交换到排序部分，直到整个列表处于排序状态。该算法在平均和最坏的情况下具有二次[时间复杂度](https://baike.baidu.com/item/时间复杂度)。

**说明：**创建一个函数并命名为`insertionSort`，输入参数是一个数组，且数组元素全部都是整数类型，然后按照从最小到最大的顺序返回整个数组。

```javascript
function insertionSort(array) {
// 请在下方区域编写代码
    let sortedLength = 1
    for (let i = 1; i < array.length; i++) {
        for (let j = 0; j <=i-1; j++) {
            if(array[i]<array[j]){
                let tmp = array[i]
                for(let k=i;k>j;k--){
                    array[k] = array[k-1]
                }
                array[j] = tmp
            }
        }
        sortedLength +=1
    }
// 请在上方区域编写代码
    console.log(array)
    return array;
}
// 测试数组：
// [1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92]
```

