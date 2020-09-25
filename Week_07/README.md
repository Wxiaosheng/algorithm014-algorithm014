# 学习笔记

## LeetCode 每日一题
* ✅  [LeetCode 538 把二叉搜索树转换为累加树](./Day1/README.md#1)
* ✅  [LeetCode 617 合并二叉树](./Day3/README.md#1)
* ✅  [LeetCode 152 乘积最大子数组](./Day4/README.md#2)
* ✅  [LeetCode 106 从中序与后序遍历序列构造二叉树](./Day5/README.md#1)

## 刷题
* ✅  二叉树的层次遍历 (过遍数)
* ✅  [LeetCode 208 实现 Trie (前缀树)](./Day2/README.md#1) （亚马逊、微软、谷歌在半年内面试中考过）
* 单词搜索 II （亚马逊、微软、苹果在半年内面试中考过）

## 实战题目
* ✅  [LeetCode 547 朋友圈](./Day4/README.md#1)（亚马逊、Facebook、字节跳动在半年内面试中考过）
* ✅  岛屿数量 (过遍数)（近半年内，亚马逊在面试中考查此题达到 361 次）
* ✅  [LeetCode 130 被围绕的区域](./Day3/README.md#2)（亚马逊、eBay、谷歌在半年内面试中考过）


## 字典树 - Tire
字典树，即 Trie 树，又称 单词查找树或键树，是一种树形结构。  
典型应用是用于统计和排序大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。  

##### 优点
最大限度地减少无谓的字符串比较，查询效率比哈希表高。

#### 基本性质
1. 节点本身不存完整的单词
2. 从根结点到某一节点，路径上经过的字符链接起来，为该节点对应的字符串
3. 每个节点的所有子节点代表的字符都不相同

#### 核心思想
Tire 树的核心思想是 **空间换时间**，利用字符串的公共前缀来降低查询时间的开销已达到提高效率的目的 


## 查并集

#### 并查集代码模板
```javascript
class UnionFind {
  constructor(n) {
    this.count = n
    this.parent = new Array(n)
    for (let i = 0; i < n; i++) {
      this.parent[i] = i
    }
  } 

  find (p) {
    let root = p
    while (root != this.parent[root]) {
      root = this.parent[root]
    }
    // 路径压缩
    while (this.parent[p] != p) {
      [p, this.parent[p]] = [this.parent[p], root]
      // let x = p
      // p = this.parent[x]
      // this.parent[x] = root
    }
    return root
  }

  union (p, q) {
    const rootP = this.find(p)
    const rootQ = this.find(q)
    if (rootP === rootQ) return
    this.parent[rootP] = rootQ
    this.count--
  }
}
```


## 高级搜索
#### DFS - 深度优先搜索代码模板
```javascript
// 递归
var dfs = function (root) {
  if (root == null) return []
  const result = []
  const helper = function (node) {
    // terminator
    if (node == null) return
    // process current logic
    helper(node.left)
    result.push(node.val)
    helper(node.right)
    // dirll down
    // restore
  }
  helper(root)
  return result
}

// 非递归
var dfs = function (root) {
  if (root == null) return []
  const result = [], statck = []
  let curr = root
  while (curr !== null || statck.length) {
    if (curr !== null) {
      statck.push(node)
      curr = curr.left
    } else {
      const node = stack.pop()
      result.push(node.val)
      curr = node.right
    }
  } 
}
```

#### BFS - 广度优先搜索代码模板
```javascript
var bfs = function (root) {
  if (root == null) return []
  const result = [], queue = [root]

  while (queue.length) {
    const n = queue.length
    for (let i = 0; i < n; i++) {
      const node = queue.shift()
      result.push(node.val)
      if (node.left) queue.push(node.left)
      if (node.right) queue.push(node.right)
    }
  }
}

// 更短
var bfs = function (root) {
  if (root == null) return []
  const result = [], queue = [[root, 0]]
  while(queue.length) {
    const [node, level] = queue.shift()
    result[level] = result[level] ? result[level] : []
    result[level].push(node.val)
    if (node.left) queue.push([node.left, level + 1])
    if (node.right) queue.push([node.right, level + 1])
  }
  return result
}
```