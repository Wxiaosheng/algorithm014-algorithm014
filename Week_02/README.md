# 学习笔记

[每日一题(置顶🔝)](../questions/README.md)

## 刷题置顶🔝
* ### 哈希表、映射、集合 - 实战题目 / 课后作业
    * ✅ [LeetCode 242 有效的字母异位词](./Day01/README.md(#1))（亚马逊、Facebook、谷歌在半年内面试中考过）
    * ✅ [LeetCode 49 字母异位词分组](./Day01/README.md#2)（亚马逊在半年内面试中常考）
    * ✅ [LeetCode 1 两数之和](./Day01/README.md#3)（亚马逊、字节跳动、谷歌、Facebook、苹果、微软、腾讯在半年内面试中常考）

* ### 树、二叉树、二叉搜索树
    * ✅ [LeetCode 94 二叉树的中序遍历](./Day2/README.md#1)（亚马逊、微软、字节跳动在半年内面试中考过）
    * ✅ [LeetCode 144 二叉树的前序遍历](./Day2/README.md#2)（谷歌、微软、字节跳动在半年内面试中考过）
    * ✅ [LeetCode 145 二叉树的后序遍历](./Day2/README.md#3)（谷歌、微软、字节跳动在半年内面试中考过）
    * ✅ [LeetCode 100 相同的树](../questions/leetcode.100.md)
    * ✅ [LeetCode 589 N叉树的前序遍历](./Day3/README.md#2)（亚马逊在半年内面试中考过）
    * ✅ [LeetCode 590 N叉树的后序遍历](./Day3/README.md#1)（亚马逊在半年内面试中考过）
    * ❌ N 叉树的层序遍历
   
* ### 堆和二叉堆
    * ✅ [剑指 Offer 40 最小的 k 个数](./Day4/README.md#1)（字节跳动在半年内面试中考过）
    * ✅ 滑动窗口最大值（亚马逊在半年内面试中常考）
    * ❌ HeapSort ：自学 https://www.geeksforgeeks.org/heap-sort/
    * ❌ 丑数（字节跳动在半年内面试中考过）
    * ❌ 前 K 个高频元素（亚马逊在半年内面试中常考）

* ### 图
    * ❌ [LeetCode 200 岛屿数量（连通图个数）]
    * ❌ [拓扑排序（Topological Sorting）](https://zhuanlan.zhihu.com/p/34871092)
    * ❌ [最短路径（Shortest Path）：Dijkstra](https://www.bilibili.com/video/av25829980?from=search&seid=13391343514095937158)
    * ❌ [最小生成树（Minimum Spanning Tree）](https://www.bilibili.com/video/av84820276?from=search&seid=17476598104352152051)
  
* ### 其他
    * ✅ [LeetCode 18 四数之和]()


## 本周预习
1. LeetCode 242 有效的字母异位词
2. LeetCode 94 二叉树的中序遍历
    * 二叉树的遍历，递归遍历、栈、莫里斯遍历
3. LeetCode 剑指 Offer 40 最小的k个数


## 第5课 哈希表、映射、集合
### 哈希表、映射、集合的实现与特性

**哈希表**（Hash table），也叫散列表，是根据**关键码值**（Key value）而直接进行访问的数据结构  

它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度，这个映射函数叫作散列函数（Hash Function），存放记录的数组叫作哈希表（或散列表）

#### 哈希碰撞(冲突)
是指 两个不通的值，通过 hash函数计算后得到结果相同，此时会新开一个链接来存储多个碰撞的值


## 第6课 树、二叉树、二叉搜索树的实现和特性

树 和 图的区别是什么？ **就看有没有形成环**

**Linked List 是特殊化的 Tree，Tree 是 特殊化的 Graph**

### 为什么会出现树？

#### 树节点的定义
```javascript 
class TreeNode {
  constructor (val) {
    this.val = val
  }
  this.left = null
  this.right = null
}
```

### 二叉树的遍历
```javascript
// 前序遍历
var preorder = function (root) {
  array.push(root.val)
  preorder(root.left)
  preorder(root.right)
}

// 中序遍历
var preorder = function (root) {
  preorder(root.left)
  array.push(root.val)
  preorder(root.right)
}

// 后序遍历
var preorder = function (root) {
  preorder(root.left)
  preorder(root.right)
  array.push(root.val)
}
```

### 二叉搜索树
二叉搜索树，也称 二叉排序树，是指一颗空树 或者具有以下性质的二叉树：
1. 左子树上 **所有节点的值** 均小于它的根结点的值
2. 右子树上 **所有节点的值** 均大于它的根结点的值
3. 以此类推，左右子树也分别是 二叉搜索树

中序遍历 => 升序遍历

### 思考题：树相关题的解法一般都是 递归，为什么？
因为 树的数据结构本身就是一种重复的结构，非常适合 递归，而不适合 循环

## 堆（Heap）
Heap： 可以迅速的找到一堆数中的最大值 或 最小值的数据结构  

将根节点最大的堆称为 大顶堆，将根节点最小的堆称为 小顶堆  

堆 其实是一种抽象的数据形式，根据实现形式可以分为 二叉堆、斐波那契堆等

### 常见 API
1. find-max: O(1) 
2. delete-max: O(logN)
3. inset(create): O(logN / O(1)

### 二叉堆（BinaryHeap）
> 完全二叉树表示非叶子节点，其子节点都是满的

通过完全二叉树来实现 （**注意，不是二叉搜索树**）

##### 性质
1. 是一颗完全树
2. 树中任意节点的值，总是 >= 其子节点的值

##### 实现
使用 一维数组，即可实现 二叉堆  

1. 根结点，即堆顶元素元素是， array[0]  
2. 索引为 i 的左孩子节点的索引是，2*i + 1
3. 索引为 i 的右孩子节点的索引是，2*i + 2
4. 索引为 i 的父节点的索引是，Math.floor((i - 1)/2)

##### 插入（insert）
1. 新元素一律插到尾部
2. 依次从 尾部向上调整整个堆的结构 (直到最顶部) （heapifyUp）

##### 删除（delete）
1. 将堆尾元素替换到顶部
2. 依次从 根部，依次向下调整整个堆的结构（直到堆尾）(heapifyDown)

**注意，二叉堆是一种堆的最常见且最简单实现，并不是最优的实现。**
