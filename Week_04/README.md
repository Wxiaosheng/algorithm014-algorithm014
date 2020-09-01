# 学习笔记

[每日一题(置顶🔝)](../questions/README.md)

## 刷题置顶🔝
* ### 递归 - 实战题目 / 课后作业
* 实战题目
    * ✅ 二叉树的层序遍历（字节跳动、亚马逊、微软在半年内面试中考过）
    * ❌ 最小基因变化
    * ✅ [LeetCode 22 括号生成](../Week_03/Day1/README.md#1)（字节跳动、亚马逊、Facebook 在半年内面试中考过）
    * ❌ 在每个树行中找最大值（微软、亚马逊、Facebook 在半年内面试中考过）
    * ❌ x 的平方根（字节跳动、微软、亚马逊在半年内面试中考过）
    * ❌ 有效的完全平方数（亚马逊在半年内面试中考过）
* 课后作业
    * ❌ 单词接龙（亚马逊在半年内面试常考）
    * ❌ 单词接龙 II （微软、亚马逊、Facebook 在半年内面试中考过）
    * ❌ 岛屿数量（近半年内，亚马逊在面试中考查此题达到 350 次）
    * ❌ 扫雷游戏（亚马逊、Facebook 在半年内面试中考过）
    * ❌ 柠檬水找零（亚马逊在半年内面试中考过）
    * ❌ 买卖股票的最佳时机 II （亚马逊、字节跳动、微软在半年内面试中考过）
    * ❌ 分发饼干（亚马逊在半年内面试中考过）
    * ❌ 模拟行走机器人
    * ❌ 跳跃游戏 （亚马逊、华为、Facebook 在半年内面试中考过）
    * ❌ 跳跃游戏 II （亚马逊、华为、字节跳动在半年内面试中考过）
    * ❌ 搜索旋转排序数组（Facebook、字节跳动、亚马逊在半年内面试常考）
    * ❌ 搜索二维矩阵（亚马逊、微软、Facebook 在半年内面试中考过）
    * ❌ 寻找旋转排序数组中的最小值（亚马逊、微软、字节跳动在半年内面试中考过）
    * ❌ 使用二分查找，寻找一个半有序数组 [4, 5, 6, 7, 0, 1, 2] 中间无序的地方


### 第9课 深度优先搜索 和 广度优先搜索

#### 深度优先搜索（DFS） - Depth First Search

按照元素的层级深度，优先遍历最左侧、最深的节点

#### DFS 递归代码模板

```javascript
var dfs = function (root) {
    // terminator
    // if (root == null) return ...
    if (visited.has(root)) return ...

    visited.add(root)
    // process current logic
    process(root)

    // drill down
    dfs(root.left)
    dfs(root.right)

    // restore
}
```

#### DFS - 非递归遍历模板

```javascript
var dfs = function (root) {
    // terminator
    // if (root == null) return ...

    const visited = new Set()
    const stack = [root]
    visited.add(root)

    while (stack.length > 0) {
        const node = stack.pop()
        if (visited.has(node)) continue
        const nodes = grentare(node)
        stack.push(nodes)
    }
}
```


#### BFS - 代码模板

```javascript
var bfs = function (root) {
    if (root == null) return []

    const queue = [root] 
    while (queue.length > 0) {
        const n = queue.length
        for (let i = 0; i < n; i++) {
            const node = queue.shift()
            // process current logic
            const nodes = grentare(node)
            queue.push(nodes)
        }
    }
}
```