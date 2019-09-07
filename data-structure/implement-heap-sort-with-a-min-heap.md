## 数据结构：在最小堆中实现堆排序

现在我们可以添加和删除元素，让我们看看堆可用于的一些应用程序。堆通常用于实现优先级队列，因为它们始终将最大值或最小值的项存储在第一个位置。此外，它们还用于实现称为堆排序的排序算法。我们将在这里看到如何做到这一点。堆排序使用最小堆，与最大堆相反。最小堆始终将最小值的元素存储在根位置。

堆排序通过获取未排序的数组，将数组中的每个项目添加到最小堆中，然后将最小堆中的每个项目提取到新数组中。最小堆结构确保新数组将包含至少最大顺序的原始项。这是最有效的排序算法之一，具有O(nlog(n))的平均和最差情况性能。

说明：让我们用最小堆实现堆排序。您可以在此处调整最大堆代码。使用insert，remove和sort方法创建一个MinHeap对象。 sort方法应返回最小堆中从最小到最大排序的所有元素的数组。

```
// check if array is sorted
function isSorted(arr) {
    var check = (i) => (i === arr.length - 1) ? true : (arr[i] > arr[i + 1]) ? false : check(i + 1);
    return check(0);
}
// generate a randomly filled array
var array = [];
(function createArray(size = 5) {
    array.push(+(Math.random() * 100).toFixed(0));
    return (size > 1) ? createArray(size - 1) : undefined;
})(25);
var MinHeap = function() {
    // 请在本行下方输入代码
    this._elems = []

    this.buildheap =function () {
        let end = this._elems.length
        for (let i = Math.floor(end/2); i >0 ; i--) {
            this.siftdown(this._elems[i],i,end)
        }
    }

    this.insert = function (e) {
        this._elems.push(e)
        this.siftup(e,this._elems.length-1)
    }

    this.siftup= function (e,last) {
        let [elems,currentIndex,parentIndex] = [this._elems,last,Math.floor((last-1)/2)]
        while(currentIndex>0 && e< elems[parentIndex] ){
            elems[currentIndex] = elems[parentIndex]
            currentIndex = parentIndex
            parentIndex =  Math.floor((parentIndex-1)/2)
        }
        elems[currentIndex] = e
    }

    this.print = function () {
        return this._elems
    }

    this.remove = function () {
        if(this._elems.length===0){
            throw new Error("MinHeap is empty!")
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
        let elems=this._elems,currentIndex = begin,childSmallerIndex = begin*2+1
        while(childSmallerIndex<end){
            if(childSmallerIndex+1<end && elems[childSmallerIndex+1]<elems[childSmallerIndex]) childSmallerIndex+=1
            if(e<elems[childSmallerIndex]) break
            elems[currentIndex] = elems[childSmallerIndex]
            currentIndex = childSmallerIndex
            childSmallerIndex = 2*childSmallerIndex+1
        }
        elems[currentIndex] = e
    }

    this.sort = function () {
        function siftdown(elems,e,begin,end) {
            let currentIndex = begin,childSmallerIndex = begin*2+1
            while(childSmallerIndex<end){
                if(childSmallerIndex+1<end && elems[childSmallerIndex+1] < elems[childSmallerIndex]) childSmallerIndex+=1
                if(e<elems[childSmallerIndex]) break
                elems[currentIndex] = elems[childSmallerIndex]
                currentIndex = childSmallerIndex
                childSmallerIndex = childSmallerIndex*2+1
            }
            elems[currentIndex] = e
        }

        let end = this._elems.length
        for (let i = Math.floor(end/2); i >=0; i--) {
            siftdown(this._elems,this._elems[i],i,end)
        }
        for (let i = end-1; i >0; i--) {
            let e = this._elems[i]
            this._elems[i] = this._elems[0]
            siftdown(this._elems,e,0,i)
        }
        return this._elems.reverse()
    }
    // 请在本行上方输入代码
};
```

