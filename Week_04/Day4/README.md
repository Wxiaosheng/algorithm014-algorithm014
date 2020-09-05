<>

<h2 id='2'>LeetCode 433 最小基因变化</h2>
一条基因序列由一个带有8个字符的字符串表示，其中每个字符都属于 "A", "C", "G", "T"中的任意一个。

假设我们要调查一个基因序列的变化。一次基因变化意味着这个基因序列中的一个字符发生了变化。

例如，基因序列由"AACCGGTT" 变化至 "AACCGGTA" 即发生了一次基因变化。

与此同时，每一次基因变化的结果，都需要是一个合法的基因串，即该结果属于一个基因库。

现在给定3个参数 — start, end, bank，分别代表起始基因序列，目标基因序列及基因库，请找出能够使起始基因序列变化为目标基因序列所需的最少变化次数。如果无法实现目标变化，请返回 -1。

注意:
1. 起始基因序列默认是合法的，但是它并不一定会出现在基因库中。
2. 所有的目标基因序列必须是合法的。
3. 假定起始基因序列与目标基因序列是不一样的。


#### 方法一：构建无向图 + BFS
> 只能用于找次数， 不能用于找路径

```javascript
var minMutation = function (start, end, bank) {
  if (bank.length == 0 || !bank.includes(end)) return -1

  const hash = new Set(bank)
  const visited = new Set()
  const queue = [start]
  visited.add(start)

  let step = 0
  while (queue.length) {
    step++
    const n = queue.length
    // 遍历 无向图 的每一层
    for (let i = 0; i < n; i++) {
      const str = queue.shift()
      // 枚举所有可能的变化
      for (let j = 0; j < 8; j++) {
        for (let c of ["A", "C", "G", "T"]) {
          const nextStr = `${str.slice(0, j)}${c}${str.slice(j + 1)}`
          if (str == nextStr) continue
          if (hash.has(nextStr)) {
            if (nextStr == end) return step
            if (!visited.has(nextStr)) {
              queue.push(nextStr)
              visited.add(nextStr)
            }
          }
        }
      }
    }
  }
  return -1
}
```

#### 优化后的 BFS
> 少了一层 BFS 固定的 for 循环，因为这里不需要处理分层，所以可以被优化掉

```javascript
var minMutation = function () {
    if (bank.length == 0 || !bank.includes(end)) return -1

  const base = ["A", "C", "G", "T"]
  const hash = new Set(bank)
  const visited = new Set()
  const queue = [[start, 0]]
  visited.add(start)

  while (queue.length) {
    const [str, count] = queue.shift()
    if (str == end) return count
    for (let i = 0; i < str.lengt; i++) {
      for (let c of base) {
        const nextStr = `${str.sicle(i, j)}${c}${str.slice(j + 1)}`
        if (nextStr == str) continue
        if (hash.has(nextStr) && !visited.has(nextStr)) {
          queue.push([nextStr, count + 1])
          visited.add(nextStr)
        }
      }
    } 
  }
  return -1
}
```

<h2 id='3'>LeetCode 108 将有序数组转换为二叉搜索树</h2>
将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

    示例:

    给定有序数组: [-10,-3,0,5,9],

    一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

          0
        / \
      -3   9
      /   /
    -10  5

#### 方法一： 自己想出来的递归

```javascript
var sortArrayToBST = function (nums) {
  if (nums.length == 0) return null
  const helper = function (node, left, right) {
    // terminator
    if (left.length == 0 && right.length == 0) return new TreeNode(node)
    // process current logic
    const root = new TreeNode(node)
    const mid1 = Math.floor(left.length / 2)
    if (left[mid1] !== undefined) {
      root.left = helper(left[mid1], left.slice(0, mid1), left.slice(mid1 + 1))
    }
    const mid2 = Math.floor(right.length / 2)
    if (right[mid1] !== undefined) {
      root.right = helper(right[mid2], right.slice(0, mid2), right.slice(mid2 + 1))
    }
    // drill down
    // restore
    return root
  }
  const mid = Math.floor(nums.length / 2)
  return helper(mid, nums.slice(0, mid), nums.slice(mid + 1))
}
```

#### 优化后的递归

```javascript
var sortedArrayToBST = function(nums) {
  if (nums.length == 0) return null

  const helper = function (nums, left, right) {
    // terminator
    if (left > right) return null
    // process current logic
    const mid = Math.floor((left + right )/ 2)
    const root = new TreeNode(nums[mid])
    root.left = helper(nums, left, mid - 1)
    root.right = helper(nums, mid + 1, right)
    // drill wodn
    // restore
    return root
  }
  return helper(nums, 0, nums.length - 1)
};
```

##### 方法二中，其实 helper 的 nums 参数没有发生过变化，所以不用做参数传递

```javascript
var sortArrayToBST = function (nums) {
    if (nums.length == 0) return null

  const helper = function (left, right) {
    // terminator
    if (left > right) return null
    // process current logic
    const mid = Math.floor((left + right) / 2)
    const root = new TreeNode(nums[mid])
    root.left = helper(left, mid - 1)
    root.right = helper(mid + 1, right)
    // drill down
    // restore
    return root
  }
  return helper(0, nums.length - 1)
}
```

<h2 id='4'>LeetCode 455 分发饼干</h2>
假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。对每个孩子 i ，都有一个胃口值 gi ，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j ，都有一个尺寸 sj 。如果 sj >= gi ，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

注意：
1. 你可以假设胃口值为正。
2. 一个小朋友最多只能拥有一块饼干。

    示例 1:

      输入: [1,2,3], [1,1]

      输出: 1

    解释: 
      你有三个孩子和两块小饼干，3个孩子的胃口值分别是：1,2,3。
      虽然你有两块小饼干，由于他们的尺寸都是1，你只能让胃口值是1的孩子满足。
      所以你应该输出1。


#### 方法一：贪心算法，先喂给刚好 或 多出孩子
> 注意，一个孩子只能拥有一块饼干🍪

```javascript
var findContentChildren = function (g, s) {
  if (g.length == 0 || s.length == 0) return 0

  let i = 0, j = 0, count = 0
  g.sort((a, b) => a - b)
  s.sort((a, b) => a - b)
  while (i < g.length && j < s.length) {
    if (g[i] <= s[j]) {
      i++, j++, count++
    } else {
      j++
    }
  }
  return count
}
```

#### j++ 可以提取到外层，上面代码优化

```javascript
var findContentChildren = function (g, s) {
  if (g.length == 0 || s.length == 0) return 0

  let i = 0, j = 0, count = 0
  g.sort((a, b) => a - b)
  s.sort((a, b) => a - b)
  while (i < g.length && j < s.length) {
    if (g[i] <= s[j]) i++, count++
    j++
  }
  return count
}
```