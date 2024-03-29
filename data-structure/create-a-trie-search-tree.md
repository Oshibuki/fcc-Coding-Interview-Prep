## 数据结构：创建一个字典树

在这里，我们将继续从二叉搜索树开始，看看另一种称为trie的树结构。 trie是一种常用于保存字符串的有序搜索树，或者更通用的关联数组或其中键是字符串的动态数据集。当许多键具有重叠前缀时，它们非常擅长存储数据集，例如，字典中的所有单词。

与二叉树不同，节点不与实际值相关联。相反，节点的路径表示特定的键。例如，如果我们想将字符串'code'存储在trie中，我们将有四个节点，每个字母对应一个节点：c - o - d - e。然后，通过所有这些节点的路径将创建'code'作为字符串 - 该路径是我们存储的密钥。然后，如果我们想要添加字符串'coding'，它将在d之后分支之前共享前三个代码节点。通过这种方式，可以非常紧凑地存储大型数据集。此外，搜索可以非常快，因为它实际上限于您存储的字符串的长度。此外，与二叉树不同，节点可以存储任意数量的子节点。

正如您可能从上面的示例中猜到的那样，一些元数据通常存储在保存密钥结尾的节点上，以便在以后的遍历中仍可以检索密钥。例如，如果我们在上面的示例中添加了代码，我们需要某种方式来知道代码中的e代表先前输入的密钥的结尾。否则，当我们添加代码时，这些信息将会丢失。

说明：让我们创建一个存储单词的trie。它将通过add方法接受单词并将它们存储在trie数据结构中。它还允许我们查询给定字符串是否是带有isWord方法的单词，并使用print方法检索输入到trie中的所有单词。 isWord应该返回一个布尔值，print应该将所有这些单词的数组作为字符串值返回。

为了让我们验证这个数据结构是否正确实现，我们为树中的每个节点提供了一个Node结构。每个节点都是一个具有keys属性的对象，该属性是JavaScript Map对象。这将保存作为每个节点的有效密钥的各个字母。我们还在节点上创建了一个end属性，如果节点表示单词的终止，则可以将其设置为true。

```
var displayTree = (tree) => console.log(JSON.stringify(tree, null, 2));
var Node = function() {
  this.keys = new Map();
  this.end = false;
  this.setEnd = function() {
    this.end = true;
  };
  this.isEnd = function() {
    return this.end;
  };
};
var Trie = function() {
  this.root = new Node();
  // 请在本行下方输入代码
  this.add=function(str){
    let letters = str.split('')
    let current=this.root
    
    for (let i = 0; i < letters.length; i++) {
      if(!current.keys.has(letters[i])){
        current.keys.set(letters[i],new Node())
      }
      current = current.keys.get(letters[i])
      
      if(i===letters.length-1){
        current.setEnd()
      }
    }

  }
  this.isWord = function(str){
    let letters = str.split('')
    let current=this.root

    for (let i = 0; i < letters.length; i++) {
      if(!current.keys.has(letters[i])){
        return false
      }
      current = current.keys.get(letters[i])
      if(i === letters.length-1 && current.isEnd()){
        return true
      }
    }
    return  false
  }

  this.print = function(){
    let words = []
    let word = '';
    let wordMaker = function(node){
      if(node.isEnd()){
        words.push(word);
      }
      let keys = [...node.keys.keys()]
      if(node.keys.size > 0){
        for(let key of keys){
          word+=key;
          wordMaker(node.keys.get(key));
        }
      }
      console.log('before slice',word)
      word = word.slice(0, -1);
      console.log('after slice',word)
    }
    wordMaker(this.root);
    return words;
  }
  // 请在本行上方输入代码
};
```

