<h2 id="1">LeetCode 208 实现 Trie (前缀树)</h2>
实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。

    示例:

    Trie trie = new Trie();

    trie.insert("apple");
    trie.search("apple");   // 返回 true
    trie.search("app");     // 返回 false
    trie.startsWith("app"); // 返回 true
    trie.insert("app");   
    trie.search("app");     // 返回 true

说明:
1. 你可以假设所有的输入都是由小写字母 a-z 构成的。
2. 保证所有输入均为非空字符串。

#### 方法一： 自己实现

```javascript
var Tire = function () {
  // 多叉树 使用 {} 的存储每一个子节点
  this.base = {}
  // 标识 当前节点是否是单词的结尾
  this.end = false
}

Tire.prototype.insert = function (word) {
  if (word.length == 0) return
  const char = word[0]
  if (word.base[char] === undefined) {
    word.base[char] = new Tire()
  }
  word.base[char].insert(word.slice(1))
}

Tire.prototype.search = function (word) {
  let tire = this
  for (let c of word) {
    if (!trie.base[c]) return false
    trie = trie.base[c]
  }
  return true
}

Tire.prototype.startWith = function (prefix) {
  let tire = this
  for (let c of prefix) {
    if (!trie.base[c]) return false
    trie = trie.base[c]
  }
  // 只要 prefix 的最后一位存在即可，不需要是单词的结尾 
  return !!trie
}
```

