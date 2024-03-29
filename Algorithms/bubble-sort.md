## 算法：冒泡排序

[冒泡排序，将是你遇到的几个排序算法中的第一个。给定一个未排序的数组，我们期望能够返回的是一个有序的数组。我们将采用不同的几种方式来实现这个功能，并且了解到不同方式的优劣之处，找到最适合的方式来实现不同的应用环境。尽管大多数的现代编程语言在内部构建了这种排序方式并提供了相应的 API，但仍然很有必要了解一些基本的方法并且知道他们是如何完成实现的](https://baike.baidu.com/item/冒泡排序)

现在我们来了解一下冒泡排序。冒泡排序方法从未排序的数组*开头*开始，并且将未排序的数组元素往后挪移，然后迭代数组，直到所有的数组元素都完全排序后才停止。这种方式是，通过比较相邻的元素然后置换元素完成排序。这种方式就是便利循环数组，直到整个数组没有元素交换为止，这样就完成了冒泡排序。这个算法的名字由来是因为越大的元素会经由交换慢慢“浮”到数列的顶端（升序或降序排列），就如同碳酸饮料中二氧化碳的气泡最终会上浮到顶端一样，故名“冒泡排序”。

这种方式通过多次迭代数组来完成操作，不管是平均还是最坏的情况，都是具有二次[时间复杂度](https://baike.baidu.com/item/时间复杂度)。尽管这个方式简单，但是在实际应用中，大多数情况下不切实际的：时间复杂度过高。

**说明：**创建一个函数并命名为`bubbleSort`，输入参数是一个数组，且数组元素全部都是整数类型，然后按照从最小到最大的顺序返回整个数组。

```javascript
function bubbleSort(array) {
// 请在下方区域编写代码
    let n = array.length
    for (let i = 0; i < array.length; i++) {
        for (let j = 0; j < n; j++) {
            if(array[j]>array[j+1]){
                [array[j],array[j+1]] = [array[j+1],array[j]]
            }
        }
        n--
    }
// 请在上方区域编写代码
    return array;
}

console.log(bubbleSort([1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92]))
```

