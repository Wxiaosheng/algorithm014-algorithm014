# 第四周 复习

## 第9课 深度优先搜索 广度优先搜索
### 深度优先搜索 - Depth First Search
代码模板 - recursion
```javascript
var dfs = function (root) {
    if (root == null) return []
    const result = [], visited = new Set()
    const helper = function (node) {
        // terminator
        if (node == null) return 
        // process current logic
        visited.add(node)
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

代码模板 - 非递归
```javascript
var dfs = function (root) {
    if (root == null) return []
    const result = [], stack = [root,] visited = new Set()
    visited.add(root)

    while (stack.length) {
        const node = stack.pop()
        result.push(node.val) // preorder
        for (let i = node.children.length; i >= 0; i++) {
            stack.push(node.children[i])
            visited.add(node.children[i])
        }
    }
    return result
}
```

### 广度优先搜索 - Breadth First Search
代码模板
```javascript
var bfs = function (root) {
    if (root == null) return []
    const result = [], queue = [root], visited = new Set()
    visited.add(root)
    while (queue.length) {
        const n = queue.length
        for (let i = 0; i < n; i++) {
            const node = queue.shift()
            result.push(node.val)
            for (let n of node.children) {
                queue.push(n)
                visited.add(n)
            }
        }
    }
    return result
}
```


实战题
1. ✅ 二叉树的层序遍历（BFS）
2. ✅ 最小基因变化 (构建无向图 + BFS)
3. ✅ 括号生成（字节跳动、亚马逊、Facebook 在半年内面试中考过）
4. ✅ 在每个树行中找最大值（微软、亚马逊、Facebook 在半年内面试中考过）

课后作业
1. ✅ 单词接龙（亚马逊在半年内面试常考）
2. 单词接龙 II （微软、亚马逊、Facebook 在半年内面试中考过）
3. ✅ 岛屿数量（近半年内，亚马逊在面试中考查此题达到 350 次）
4. 扫雷游戏（亚马逊、Facebook 在半年内面试中考过）


## 第10课 贪心算法

课后作业
1. ✅ 柠檬水找零（greedy）
2. ✅ 买卖股票的最佳时机 II （greedy）
3. ✅ 分发饼干（greedy）
4. ✅ 模拟行走机器人 (if-else + loop)
5. ✅ 跳跃游戏 （确定能到的最大位置）
6. 跳跃游戏 II （亚马逊、华为、字节跳动在半年内面试中考过）


## 第11课 二分查找

实战题目
1. ✅ x 的平方根（Binary Search）
2. ✅ 有效的完全平方数（Binary Search）

课后作业
1. ✅ 搜索旋转排序数组（Binary Search）
2. ✅ 搜索二维矩阵（Binary Search）
3. ✅ 寻找旋转排序数组中的最小值（Binary Search）
4. 使用二分查找，寻找一个半有序数组 [4, 5, 6, 7, 0, 1, 2] 中间无序的地方


#### Binary Search 代码模板

1. 标准 Binary Search 模板

```javascript
var bs = function (nums, target) {
    if (nums.length == 0) return false

    let left = 0, right = nums.length - 1
    while (left <= right) {
        const mid = Math.floor((left + right) / 2)
        if (nums[mid] == target) {
            return true
        } else if (nums[i] < target) {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
}
```

2. 旋转排序数组模板

```javascript
var xzbs = function (nums) {
    if (nums.length == 0) return false

    let left = 0, right = nums.length - 1
    while (left <= right) {
        const mid = Math.floor((left + right) / 2)
        // mid 可能是最小值
        if (nums[mid] < nums[right]) right = mid
        else left = mid + 1
    }
    return nums[left]
}
```

3. 有效的完全平方数

```javascript
var isPerfectSquare = function (num)  {
  if (num < 2) return num

  let left = 0, right = num - 1
  while (left <= right) {
    const mid = Math.floor((left + right) / 2) 
    const curr = mid * mid
    if (curr == num) return true
    if (curr > num) right = mid - 1
    if (curr < num) left = mid + 1
  }
  return false
}
```