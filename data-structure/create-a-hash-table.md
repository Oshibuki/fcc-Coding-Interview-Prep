## 数据结构：创建一个哈希表

在本次挑战中我们会学习哈希表。与对象和 Map 类似，hash 也可以用来实现关联数组或者匹配的键值对。在 JavaScript 中，我们可以用对象来实现哈希表（具体实现方式依赖于运行环境）。哈希表接收一个 key 作为参数，并以特定的方式把 key 转换为一串数字。该数字串会与 value 值建立对应关系，并存储到表中。如果你想获取该 key 值，hashing 函数会接收 key 作为参数，并经过计算后得到与存储时的 key 相同的数字串，然后通过该数字串获取对应的 value。这种查询方式非常高效，平均时间复杂度为 O(n)。

我们还可以用数组来实现哈希表，该数组拥有一个 hash 方法，用于在指定区间内生成一系列索引。在此方法中，数组的长度和 hash 函数的选择都很关键。试想一下，假如两个不同的 key 值通过同一个 hash 函数产生了相同的值怎么办？我们称这种情况为 collision（冲突）。解决冲突的一种方式是将键值对存入该 index 中。在查询时，你需要遍历一下这个 index 上存储的所有数据，找出你需要的那一条。一个好的 hash 函数应维持较低的冲突发生率，以保证查询效率。

本课程我们不关注 hash 函数或者哈希表的实现细节，熟悉一下他们是如何运作的即可。

挑战说明：现在我们来创建一个拥有基本功能的哈希表。我们已经为你写好了一个简单的 hash 函数，当你传递一个值给该函数时，它会返回一个经过 hash 运算的值；你需要用这个值作为 key，将元素存储到 this.collection 对象中。然后，你需要其中创建 add、remove、lookup 这三个方法。add 方法接收一个键值对参数并把它存储到哈希表中；remove 方法接收一个 key 为参数并移除对应的键值对；lookup 方法接收一个 key 为参数并返回对应的 value 值，如果 key 值不存在就返回 null。

请确保你的代码能处理发生冲突的情况。

```
var called = 0;
var hash = (string) => {
  called++;
  var hash = 0;
  for (var i = 0; i < string.length; i++) { hash += string.charCodeAt(i); }
  return hash;
};
var HashTable = function() {
  this.collection = {};
  // 请把你的代码写在这条注释以下
  this.add = function(key,value){
      let hashCode = hash(key)
      if(this.collection.hasOwnProperty(hashCode)){
        this.collection[hashCode][key] = value
      }else{
        this.collection[hashCode] = {}
        this.collection[hashCode][key] = value
      }
  }
  this.remove =function(key){
      let hashCode = hash(key)
      delete this.collection[hashCode][key]
  }
  this.lookup = function(key){
      let hashCode = hash(key)
      if(this.collection.hasOwnProperty(hashCode) && this.collection[hashCode].hasOwnProperty(key)){
        return this.collection[hashCode][key]
      }else{
          return null
      }
  }
  // 请把你的代码写在这条注释以上
};
```

