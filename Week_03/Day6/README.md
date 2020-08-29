<h2 id='1'>LeetCode 77 组合</h2>
给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

    示例:

    输入: n = 4, k = 2
    输出:
    [
        [2,4],
        [3,4],
        [2,3],
        [1,2],
        [1,3],
        [1,4],
    ]

#### 方法一、两层 暴力循环

```javascript
var combine = function (n, k) {
    if (k == 0) return []
    const result = []
    for (let i = 1; i < n; i++) {
        for (let  j = i + 1; j <= n; j++) {
            result.push([i, j])
        }
    }
    return result
}
```

#### 方法二、递归 - 回溯

```javascript
var combine = function (n, k) {
    if (k == 0) return []
    const result = []
    const helper = function (level, sub) {
        // terminator
        if (sub.length >= k) return result.push(sub.slice(0))
        // process current logic
        for (let i = level; i <= n; i++) {
            sub.push(i)
            // drill down
            helper(i + 1, sub)
            // restore
            sub.pop()
        }
    }
    helper(1, [])
    return result
}
```

在看一种，类似生成括号、子集的通用解法，**选或不选的思想**

```javascript
var combine = function(n, k) {
  if (k == 0) return []
  const result = []
  const helper = function (level, sub) {
    // terminator
    if (sub.length == k) return result.push(sub.slice(0))
    if (level > n || sub.length > k) return
    // process current logic
    helper(level + 1, sub) // 不选
    sub.push(level)
    helper(level + 1, sub) // 选
    // drill down
    // restore
    sub.pop()
  }
  helper(1, [])
  return result
};
```

<h2 id="2">LeetCode 46 全排列</h2>
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

#### 方法一、三层暴力循环， 不用写，肯定超时

#### 方法二、递归

```javascript
var permute = function(nums) {
  if (nums.length == 0) return []
  const result = []
  const helper = function (level, sub) {
    // terminator
    if (level >= nums.length) return result.push(sub.slice(0))
    // process current logic
    for (let i = 0; i < nums.length; i++) {
      if (sub.indexOf(nums[i]) > -1) continue
      helper(level + 1, [...sub, nums[i]])
    }
    // drill down
    // restore
  }
  helper(0, [])
  return result
};
```

#### 方法三、回溯

```javascript
var permute = function(nums) {
  if (nums.length == 0) return []
  const result = []
  const helper = function (level, sub) {
    // terminator
    if (sub.length == nums.length) return result.push(sub.slice(0))
    // process current logic
    for (let i = 0; i < nums.length; i++) {
      if (sub.includes(nums[i])) continue
      sub.push(nums[i])
      helper(level + 1, sub)
      sub.pop()
    }
    // drill down
    // restore
  }
  helper(0, [])
  return result
};
```

<h2 id="3">LeetCode 46 全排列II</h2>

给定一个可包含重复数字的序列，返回所有不重复的全排列。

    示例:

    输入: [1,1,2]
    输出:
    [
        [1,1,2],
        [1,2,1],
        [2,1,1]
    ]

