## 算法：更新库存

创建一个[二维数组](https://baike.baidu.com/item/二维数组)，比较并更新存储在`二维数组`中的“库存”元素，然后并将其与新产生的第二个二维数组进行对比，更新当前的 ”库存“ 项的数量（`arr1`），如果找不到这个对比对象，那么将新的对象和数量添加到“库存”数组中。注意：返回的“库存”数组应该是按照数组元素的首字母顺序排序

```javascript
function updateInventory(arr1, arr2) {
    // 提取第二个元素，成为一个新数组 valueArr
    var valueArr = arr1.map(function(e) {
        return e[1]
    });
    for (var i = 0; i < arr2.length; i++) {
        var index = valueArr.indexOf(arr2[i][1])
        if (index > -1) {
            arr1[index][0] += arr2[i][0];
        } else {
            arr1.push(arr2[i]);
        }
    }
    return arr1.sort(function(a, b) {
        return a[1] > b[1] ? 1 : -1;
    });
}

var curInv = [
    [21, "Bowling Ball"],
    [2, "Dirty Sock"],
    [1, "Hair Pin"],
    [5, "Microphone"]
];

var newInv = [
    [2, "Hair Pin"],
    [3, "Half-Eaten Apple"],
    [67, "Bowling Ball"],
    [7, "Toothpaste"]
];

console.log(updateInventory(curInv, newInv))
```

