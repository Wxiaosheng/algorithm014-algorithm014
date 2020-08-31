<h2 id="1">LeetCode 657 机器人能否返回原点</h2>

在二维平面上，有一个机器人从原点 (0, 0) 开始。给出它的移动顺序，判断这个机器人在完成移动后是否在 (0, 0) 处结束。

移动顺序由字符串表示。字符 move[i] 表示其第 i 次移动。机器人的有效动作有 R（右），L（左），U（上）和 D（下）。如果机器人在完成所有动作后返回原点，则返回 true。否则，返回 false。

注意：机器人“面朝”的方向无关紧要。 “R” 将始终使机器人向右移动一次，“L” 将始终向左移动等。此外，假设每次移动机器人的移动幅度相同。

    示例 1:

    输入: "UD"
    输出: true
    解释：机器人向上移动一次，然后向下移动一次。所有动作都具有相同的幅度，因此它最终回到它开始的原点。因此，我们返回 true。示例 1:


#### 方法一、loop 记录
通过遍历机器人走过的路径，分别记录 横向 和 纵向的距离

```javascript
var  judgeCircle = function (moves) {
  if (moves.length == 0) return 0
  let row = 0, col = 0;
  for (let s of moves) {
    if (s == 'R') row++
    if (s == 'L') row--
    if (s == 'U') col++
    if (s == 'D') col--
  }
  return row == 0 && col == 0
}
```

<h2 id="2">LeetCode 77 组合</h2>

给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

    示例:
    输入: n = 4, k = 2
    输出:
    [
      [2,4],
      [3,4],
      [2,3],
      [1,2],
      [1,3],
      [1,4],
    ]

#### 方法一、泛型递归

```javascript
var combine = function (n, k) {
  if (k == 0) return []
  // 泛型递归
  const result = []
  const helper = function (level, s) {
    // terminator
    if (level >= k) return result.push(s)
    // process current logic
    // 此行为第二次减枝 通过，(组合的结果是递增的，所以后面的元素一定比前面的元素大)
    const start = s[s.length - 1] === undefined ? 1 : s[s.length - 1]
    // 第三次减枝，提升新能 (当前结果+可遍历的数值个数都小于k，则不必在继续循环下去)
    if (n - start + 1 + s.length < k) return
    for (let i = start; i <= n; i++) {
      const copy_s = JSON.parse(JSON.stringify(s))
      // 此行为第一次减枝，但是还是运行超时 (去重)
      if (copy_s.indexOf(i) > -1) continue
      if (copy_s.length > 0 && i <= copy_s[copy_s.length - 1]) continue
      copy_s.push(i)
      helper(level + 1, copy_s)
    }
    // drill down
    // restore
  }
  helper(0, [])
  return result
}
```

#### 方法二、回溯

**回溯的代码模板：**

    const helper = function (level, 当前结果) {
      if (满足条件) return 保存当前结果
      for (let 选择 of 选择列表) {
        当前结果.add(选择)
        helper(下一层， 当前结果(改变后的)
        当前结果.pop()
      }
    }

```javascript
var combine = function (n, k) {
  const result = []
  const helper = function (level, r) {
    // terminator
    // 这里存的是 r 的引用地址，所以必须存储当前结果的副本
    if (r.length >= k) return result.push(r.slice())
    // process current logic
    for (let i = level; i <= n; i++) {
      r.push(i)
      helper(i + 1, r)
      r.pop()
    }
    // drill down
    // restore
  }
  helper(1, [])
  return result
}
```


<h2 id="3">LeetCode 46 全排列</h2>
给定一个 没有重复 数字的序列，返回其所有可能的全排列。

    示例:
    输入: [1,2,3]
    输出:
    [
      [1,2,3],
      [1,3,2],
      [2,1,3],
      [2,3,1],
      [3,1,2],
      [3,2,1]
    ]
  
#### 方法一、递归 - 回溯

```javascript
var permute = function (nums) {
  const n = nums.length
  const result = []
  const helper = function (sub) {
    // terminator 
    if (sub.lengt >= n) return result.push(sub.slice(0))
    // process current logic
    for (let i = 0; i < n; i++) {
      // 去除重复元素
      if (sub.indexOf(nums[i]) > -1) continue
      sub.push(nums[i])
      helper(sub)
      sub.pop()
    }
    // drill down
    // restore
  }
  helper([])
  return result
}
```

**与 LeetCode 77 组合 相比，全排列的递归方法少了一个参数，并且 `for` 循环的起始条件不同， 这是因为： 组合 的结果需要有序，而全排列则不需要有序**
