## 算法：合并排序

另一种非常常见的排序方式是[归并排序。如同快速排序一样，归并排序也是采用了分而治之的递归方法来排序数组。它利用了这么一个现象，即只要首先对两个数组进行排序，就比较容易对他们进行排序。但是我们的参数只能一个数组，那么又将如何从这个数组中得到两个排序数组呢？我们可以递归的将原始数组一分为二，直到数组里面只包含一个元素为止。单个元素的数组是自然排序的，所以我们可以开始合并。这种合并方式是将拆分的原始数组进行递归调用，最后将所有的元素生成一个最终的排序数组。](https://baike.baidu.com/item/归并排序)

合并的步骤是：

**1)**：递归的将输入数组拆分成两个子数组，直到所有的子数组都只包含一个元素。

**2)**：将每一个排序后的子数组合并到一个数组里面，最后返回一个排序的数组。

归并排序是一种高效的排序方式，[时间复杂度](https://baike.baidu.com/item/时间复杂度)为*O(nlog(n))*。因为归并排序的性能优良且相对容易实现，所有这种排序方式很受欢迎。

另外，这将是我们在此章节讨论的最后一种排序算法，但是在后续有关**树型数据结构**的章节中，我们将一起研究**堆排序**，同样它也是一种高效的排序方式，其实现过程需要用到二进制堆的概念。

**Instructions**：创建一个函数并命名为`mergeSort`，输入参数是一个数组，且数组元素全部都是整数类型，然后按照从最小到最大的顺序返回整个数组>。实现这个排序方式可以采用两个函数来实现：`merge`负责合并两个排序的数组，`merge sort`负责生成单个数组的用于归并使用。祝你好运！

```javascript
function mergeSort(array,start=0,end=array.length-1) {
    // 要排序的数组是 a[low..high]
    if (start < end) { // base case: low >= high (0 or 1 item)
        let mid =Math.floor( (start+end)/ 2);
        mergeSort(array, start  , mid ); // 分成一半
        mergeSort(array, mid+1, end); // 递归地将它们排序
        merge(array, start, mid, end); // 解决: 归并子程序
    }
    return array
}


function merge(array,start,middle,end){
    let leftArrayLength = middle-start+1,
        rightArrayLength = end-middle;

    let leftArray=[],rightArray=[]

    //fill in leftArray
    for (let i = 0; i < leftArrayLength; ++i)
        leftArray[i] = array[start + i]

    // fill in right array
    for (let i = 0; i < rightArrayLength; ++i)
        rightArray[i] = array[middle + 1 + i]

    // merge the temp arrays

    // initial indexes of first and second subarrays
    let leftIndex = 0, rightIndex = 0

    // the index we will start at when adding the subarrays back into the main array
    let currentIndex = start;
    // compare each index of the subarrays adding the lowest value to the currentIndex
    while (leftIndex < leftArrayLength && rightIndex < rightArrayLength) {
        if (leftArray[leftIndex] <= rightArray[rightIndex])
            array[currentIndex] = leftArray[leftIndex++]
        else
            array[currentIndex] = rightArray[rightIndex++]
        currentIndex++
    }

    // copy remaining elements of leftArray[] if any
    while (leftIndex < leftArrayLength) array[currentIndex++] = leftArray[leftIndex++]

    // copy remaining elements of rightArray[] if any
    while (rightIndex < rightArrayLength) array[currentIndex++] = rightArray[rightIndex++]
}

let array = [1, 4,43, 32, 2, 8, 345, 123]
mergeSort(array)
console.log(array)
```

