# 学习笔记

## LeetCode 每日一题
* ✅  [LeetCode 538 把二叉搜索树转换为累加树](./Day1/README.md#1)
* ✅  [LeetCode 617 合并二叉树](./Day3/README.md#1)
* ✅  [LeetCode 152 乘积最大子数组](./Day4/README.md#2)
* ✅  [LeetCode 106 从中序与后序遍历序列构造二叉树](./Day5/README.md#1)
* ✅  [LeetCode 16 最接近的三数之和](./Day6/README.md#1)


## 实战题目
* ✅  (过遍数) 二叉树的层次遍历
* ✅  [LeetCode 208 实现 Trie (前缀树)](./Day2/README.md#1) （亚马逊、微软、谷歌在半年内面试中考过）
* ✅  (过遍数) 岛屿数量 （近半年内，亚马逊在面试中考查此题达到 361 次）
* 二进制矩阵中的最短路径（亚马逊、字节跳动、Facebook 在半年内面试中考过）
* 滑动谜题（微软、谷歌、Facebook 在半年内面试中考过）

## 本周作业
### 简单
* ✅  (过遍数) 爬楼梯（阿里巴巴、腾讯、字节跳动在半年内面试常考）
### 中等
* ✅  [LeetCode 208 实现 Trie (前缀树)](./Day2/README.md#1) (前缀树) （亚马逊、微软、谷歌在半年内面试中考过）
* ✅  [LeetCode 547 朋友圈](./Day4/README.md#1)（近半年内，亚马逊在面试中考查此题达到 361 次）
* ✅  [LeetCode 130 被围绕的区域](./Day3/README.md#2)（亚马逊、eBay、谷歌在半年内面试中考过）
* ✅  [LeetCode 36 有效的数独](./Day7/README.md#1)（亚马逊、苹果、微软在半年内面试中考过）
* ✅  (过遍数) 括号生成（亚马逊、Facebook、字节跳动在半年内面试中考过）
* 单词接龙（亚马逊、Facebook、谷歌在半年内面试中考过）
* 最小基因变化（谷歌、Twitter、腾讯在半年内面试中考过）
### 困难
* 单词搜索 II （亚马逊、微软、苹果在半年内面试中考过）
* N 皇后（亚马逊、苹果、字节跳动在半年内面试中考过）
* 解数独（亚马逊、华为、微软在半年内面试中考过）

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


## 查并集 - Disjoint Set
适用场景： **组团、配对 问题**

### 基本操作
1. makeSet(n)  
    建立一个新的并查集，其中包含 n 个元素集合
2. unionSet(x, y)  
    把元素 x 和 元素 y 所在的集合合并，要求 x，y 所在的集合不相交，如果相交则不合并
3. find(x)  
    找到元素 x 所在集合的代表，该操作也可以用来**判断两个元素是否在同一集合**

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
### 减枝
例如，国际象棋、井字棋、象棋、围棋 等
#### 回溯法
回溯法采用试错的思想，它尝试分步的去解决一个问题。  
在分步解决问题的过程中，发现现有的分步不能解决问题时，会返回上一步，甚至是上几步

### 双向 BFS

### 启发式搜索
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

###  启发式搜索 Heuristic Search (A*)
#### 估价函数
启发式函数: h(n)，它用来评价哪些结点最有希望的是一个我们要找的结 点，h(n) 会返回一个非负实数,也可以认为是从结点n的目标结点路径的估 计成本。  
启发式函数是一种告知搜索方向的方法。它提供了一种明智的方法来猜测 哪个邻居结点会导向一个目标。  


## 高级树、AVL 树和红黑树

### 二叉搜索树 - Binary Search Tree
> all left < root < all right

#### 存在的问题
当极端情况下，二叉搜索树会退化成 链表结构。  
保证性能的关键：搜索的效率是取决于树的深度的，因此平衡左右子树即可。

### AVL 树
`Balance Factor` (平衡因子):   
是它的左子树的高度减去它的右子树的高度(有时相反)。 balancefactor={-1, 0, 1}

#### 通过旋转操作来进行平衡(四种)
1. 左旋  
    子树形态:右右子树 —>左旋
2. 右旋  
    子树形态:左左子树 —>右旋
3. 左右旋  
    子树形态:左右子树 —>左右旋
4. 右左旋  
    子树形态:左右子树 —>左右旋

注意： 带有子树的旋转时，需要处理 **旋转结点右子树**


### 红黑树 -  Red-black Tree
红黑树是一种近似平衡的二叉搜索树(Binary Search Tree)，它能够确保任何一 个结点的左右子树的高度差小于两倍。

红黑树是满足如下条件的二叉 搜索树: 
1. 根结点是黑色
2. 每个叶结点(NIL结点，空结点)是黑色的
3. 不能有相邻接的两个红色结点
4. 从任一结点到其每个叶子的所有路径都包含相同数目的黑色结点

#### 关键性质
从根到叶子的最长的可能路径不多于最短的可能路径的两倍长。

#### AVL Tree 与 Red-black Tree 对比
AVL Tree 是严格的平衡二叉树，因此插入和删除的效率低，而查询和搜索的效率高    
Red-black Tree 是近似平衡二叉树，插入和删除的效率高，而 查询和搜索的效率低  

