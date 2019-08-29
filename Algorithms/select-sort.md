## 算法：选择排序

现在我们开始实现[选择排序](https://baike.baidu.com/item/选择排序)。选择排序是通过选择列表中最小值来与列表中的第一个值进行对比交换，然后从第二位置开始逐一对比，选择剩下的列表中最小值与第二个元素交换位置。然后循环遍历列表并交换元素，直到列表最后一个元素，此时的列表就完成了排序。选择排序在所有的情况下都具有二次[时间复杂度](https://baike.baidu.com/item/时间复杂度)。

**说明：**创建一个函数并命名为`selectionSort`，输入参数是一个数组，且数组元素全部都是整数类型，然后按照从最小到最大的顺序返回整个数组。

```javascript
function selectionSort(array) {
// 请在下方区域编写代码
    for (let i = 0; i < array.length - 1; i++) {
        let min = array[i],minIndex =i
        for (let j = i + 1; j < array.length; j++) {
            if (min > array[j]) {
                min = array[j];
                minIndex = j
            }
        }
        [array[i],array[minIndex]] =[ array[minIndex],array[i]]
    }
// 请在上方区域编写代码
    return array;
}
```

