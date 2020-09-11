学习笔记

复习过程中，发现的个人不熟练的题目：
* LeetCode 11 盛水最多的容器
* LeetCode 84 柱状图中最大的矩形
* LeetCode 42 接雨水
* LeetCode 206 反转链表
* LeetCode 24 两两交换链表中的节点
* LeetCode 25 K 个一组翻转链表
* LeetCode 433 最小基因变化
* LeetCode 55 跳跃游戏


* 二叉树遍历 - 代码模板
  * BFS 两种迭代形式
  * DEF 递归 + 迭代
* N叉树遍历
  * 前序 递归 + 迭代
  * 后续 递归 + 迭代


树的遍历 - 代码模板

二叉树遍历
BFS
```javascript
var bfs1 = funct ion (root) {
    if (root == null) return []
    const result = []
    const queue = [root] 
    while (queue.length) {
        const n = queue.length, sub = []
        for (let i = 0; i < n; i++) {
            const node = queue.shift()
            sub.push(node.val)
            if (node.left) queue.push(node.left)
            if (node.right) queue.push(node.right)
        }
        result.push(sub)
    }
    return result
}
```

```javascript
var bfs2 = function (root) {
    if (root == null) return []
    const reuslt = []
    const queue = [[root, 1]]
    while (queue.lenght) {
        const [node, level] = queue.shift()
        result[level] = result[level] === undefined ? [] : result[level]
        result[level].push(node.val)
        if (node.left) queue.psuh(node.left)
        if (node.right) queue.push(node.right)
    }
    return result
}
```

```javascript
var dfs = function (root) {
    if (root == null) return []
    const result = []
    const helper = fucntion (node) {
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
```

```javascript
var dfs = function (root) {
    if (root == null) return []
    const reuslt = [], stack = []
    let curr = root
    while (curr !== null || stack.length) {
        if (curr !== null) {
            stack.push(curr)
            curr = curr.left
        } else {
            const node = stack.pop()
            result.push(node.val)
            curr = node.right
        }
    }
    return result
}
```

N叉的遍历
```javascript
var bfs = function (root) {
    if (root == null) return []
    const result = []
    const queue = [root]
    while (queue.length) {
        const n = queue.length, sub = []
        for (let i = 0; i < n; i++) {
            const node = queue.shift()
            sub.push(node.val)
            for (let n of node.children) {
                queue.push(n)
            }
        }
        result.push(sub)
    }
    return result
}
```

```javascript
var dfs = fucntion (root) {
    if (root == null) return []
    const result = []
    const helper = function (root) {
        // terminator
        if (root == null) return
        // process current logic
        result.push(node.val)
        for (let n of node.children) {
            helper(n)
        }
        // drill down
        // restore
    }
    helper(root)
    return result
}
```

```javascript
// preorder
var bfs = fucntion (root) {
    if (root == null) return []
    const result = []
    const stack = [root]
    while (stack.length) {
        const node = stack.pop()
        result.push(node.val)
        for (let i = node.children.length; i >= 0; i--) {
            stack.push(node.children[i])
        }
    }
    return result
}
```

```javascript
// postorder 
var dd = function (root) {
    if (root == null) return []
    const result = []
    const stack = [root]
    while (stack.length) {
        const node = stack.pop()
        result.push(node.val)
        for (let n of node.children) {
            stack.push(n)
        }
    }
    return result.reverse()
}
```
