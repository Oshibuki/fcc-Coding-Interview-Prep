## 算法：快速排序

现在我们开始讨论[快速排序。快速排序是一种高效的递归分治方法来排序数组。在这个方法中，需要在原始数组中选择一个枢轴值，然后将数组划分为两个子数组，其值大于或者小于枢轴值，然后我们将递归调用两个子数组上的快速排序算法的结果来配合使用，直到空数组或者单个元素的数组的情况，然后返回结果。递归调用的展开结果将返回的是排序后的数组。](https://baike.baidu.com/item/快速排序算法?fromtitle=快速排序&fromid=2084344)

快速排序是一种非常有效的排序方式，平均[时间复杂度](https://baike.baidu.com/item/时间复杂度)为*O(nlog(n))*，同时它也是相对比较容易实现的方式。这些特性使得快速排序成为了一种流行而有用的排序方式。

**说明：**创建一个函数并命名为`quickSort`，输入参数是一个数组，且数组元素全部都是整数类型，然后按照从最小到最大的顺序返回整个数组。虽然选择一个枢轴值很重要，但任何一个枢轴都能满足要求，为了以防万一，我嘛一般选择第一个或者最后一个元素来作为数轴值。

```javascript
function quickSort(array) {
// 请在下方区域编写代码
    if(array.length <2){
        return array
    }
    const [head,...tails] = array,
        left= tails.filter(i=> i<head),
        right=tails.filter(i=> i>=head)

    return quickSort(left).concat(head,quickSort(right))

// 请在上方区域编写代码
    return array;
}

// 测试函数：
// [1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92]
```

