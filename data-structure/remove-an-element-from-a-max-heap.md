## 数据结构：从最大堆中删除一个元素

现在我们可以向堆中添加元素，让我们看看如何删除元素。删除和插入元素都需要类似的逻辑。在最大堆中，您通常需要删除最大值，因此这只需要从树的根中提取它。这将破坏我们树的堆属性，因此我们必须以某种方式重新建立它。通常，对于最大堆，这可以通过以下方式完成：

将堆中的最后一个元素移动到根位置。

如果root的子节点大于它，则将root与较大值的子节点交换。

继续交换，直到父级大于两个子级，或者到达树中的最后一级。

说明：向我们的最大堆添加一个名为remove的方法。此方法应返回已添加到最大堆的最大值，并将其从堆中删除。它还应该重新排序堆，以便保持堆属性。删除元素后，堆中剩余的下一个最大元素应该成为根。此处再次添加插入方法。

```
var MaxHeap = function(list=[]) {
  // 请在本行下方输入代码
  this._elems = Array.from(list)
    this.remove = function () {
    if(this._elems.length===0){
      throw new Error("MaxHeap is empty!")
    }
    let elems = this._elems,
        elem0=elems[0],
        e = elems.pop()
    if(elems.length>0){
      this.siftdown(e,0,elems.length)
    }
    return elem0
  }


  this.siftdown = function (e,begin,end) {
    let elems=this._elems,currentIndex = begin,childLargerIndex = begin*2+1
    while(childLargerIndex<end){
      if(childLargerIndex+1<end && elems[childLargerIndex+1]>elems[childLargerIndex]) childLargerIndex+=1
      if(e>elems[childLargerIndex]) break
      elems[currentIndex] = elems[childLargerIndex]
      currentIndex = childLargerIndex
      childLargerIndex = 2*childLargerIndex+1
    }
    elems[currentIndex] = e
  }

    this.insert = function (e) {
    this._elems.push(e)
    this.siftup(e,this._elems.length-1)
  }

  this.siftup= function (e,last) {
    let [elems,currentIndex,parentIndex] = [this._elems,last,Math.floor((last-1)/2)]
    while(currentIndex>0 && e> elems[parentIndex] ){
      elems[currentIndex] = elems[parentIndex]
      currentIndex = parentIndex
      parentIndex =  Math.floor((parentIndex-1)/2)
    }
    elems[currentIndex] = e
  }

  this.print = function () {
    return this._elems
  }
  // 请在本行上方输入代码
};
```

