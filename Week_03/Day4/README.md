<h2 id="1">LeetCode 50 Pow(x, n)</h2>
实现 pow(x, n) ，即计算 x 的 n 次幂函数。

    示例 1:
    输入: 2.00000, 10
    输出: 1024.00000

    示例 2:
    输入: 2.10000, 3
    输出: 9.26100

    示例 3:
    输入: 2.00000, -2
    输出: 0.25000
    解释: 2-2 = 1/22 = 1/4 = 0.25

说明:
* -100.0 < x < 100.0
* n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。


#### 方法一、数学定义法
1. x 的 n 次幂，表示 n 个 x 相乘
2. 当 n < 0 时，表示 n 个 1/x 相乘

```javascript
var myPow = function (x, n) {
    if (n == 0) return 0
    if (x == 0) return 1
    if (n < 0) x = 1 / x
    let result = 1
    for (let i = 0; i < n; i++) {
        result *= x
    }
    return result
}
```

**注意，本方法的时间复杂度为 O(N)，但是实际上，计算x 的 n 次幂时，无需一个一个的 x 相乘，比如 2^10，可以拆解成 2^5 * 2^5**


#### 方法二，拆分指数
> 时间复杂度能降低到 O(lognN)

```javascript
var myPow = function (x, n) {
    if (x == 0) return 0
    if (n == 0) return 1
    if (n < 0) {
      x = 1/x
      n = -n
    }
    const subResult = myPow(x, Math.floor(n / 2))
    return n % 2 == 0 ? subResult * subResult : subResult * subResult * x
}
```


<h2 id="2">LeetCode 78 子集</h2>
给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

    示例:
    输入: nums = [1,2,3]
    输出:
    [
      [3],
      [1],
      [2],
      [1,2,3],
      [1,3],
      [2,3],
      [1,2],
      []
    ]

#### 方法一，递归

    []      => []
    [1]     => [], [1]
    [1,2]   => [], [1], [2], [1,2]
    [1,2,3] => [], [1], [2], [1,2], [3], [1,3], [2,3], [1,2,3]

    通过观察，可以发现，下一层的结果，都是将上一层的结果每一个元素都加新元素 和 上一层原来的结果 总和

```javascript
var subsets = function (nums) {
  if (nums.length == 0) return []
  const helper = function (level, result) {
    // terminator
    if (level >= nums.length) return result
    // process current logic
    const copyPrev = JSON.parse(JSON.stringify(result))
    for (let i = 0; i < copyPrev.length; i++) {
      copyPrev[i].push(nums[level])
    }
    // drill dowm
    return helper(level + 1, [...result, ...copyPrev])
    // restore 
  }
  return helper(0, [[]])
}
```

#### 方法二、本题类似于 括号生成的问题
可以看成对传进来的数组做遍历，对于每个元素都有选和不选两种操作，这样就可以得到最终结果

```javascript

var subsets = function (nums) {
  if (nums.length == 0) return []
  const result = []
  const helper = function (level, sub) {
    // terminator
    if (level >= nums.length) return result.push(sub.slice(0))
    // process current logic
    // 不选
    helper(level + 1, sub)
    // 选
    sub.push(nums[level])
    helper(level + 1, sub)
    // drill down 
    // restore - 由于 sub 是函数的参数，传递的是引用地址，因此需要回复本层 对 sub 影响
    sub.pop()
  }
  helper(0, [])
  return result
}
```

#### 方法三、迭代

```javascript
var subsets = function (nums) {
  if (nums.length == 0) return []
  let result = [[]]
  for (let i = 0; i < nums.length; i++) {
    const prev = JSON.parse(JSON.stringify(result))
    for (let c of prev) {
      c.push(nums[i])
    }
    result = result.concat(prev)
  }
  return result
}
```

#### 方法三、另一种递归思想
类似这种组合的问题，有一种通用的递归 组合方式

1. 获取子集，可以看成对数组中的每一个元素，有 取 或者 不取 两种操作
2. 递归，对每一元素都进行 取 或者 不取 的操作

应用：
  1. 生成有效括号也是类似这种思想（放左括号或者放右括号）

```javascript
var subsets = function (nums) {
  if (nums.length == 0) return []
  const helper = function (level, result) {
    // terminator
    if (level >= nums.length) return [result]
    // process current logic
    const no = helper(level + 1, JSON.parse(JSON.stringify(result)))
    // 取
    result.push(nums[level])
    const take = helper(level + 1, JSON.parse(JSON.stringify(result)))
    // drill down
    // restore
    return [...no, ...take]
  }
  return helper(0, [[]])
}
```

<h2 id="3">LeetCode 169 多数元素</h2>
给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

#### 方法一、遍历数组 + Map 计数

```javascript
var majorityElement = function (nums) {
  const hashMap = {}
  for (let i of nums) {
    hashMap[i] = hashMap[i] === undefined ? 1 : hashMap[i] + 1
    if (hashMap[i] > Math.floor(nums.length / 2)) return i
  }
}
```

#### 方法二、排序取中间的元素
> 前提：数组是非空的，并且给定的数组总是存在多数元素

```javascript
var majorityElement = function (nums) {
  return nums.sort((a, b) => a - b)[Math.floot(nums.length / 2)]
}
```

<h2 id="4">LeetCode 17 电话号码的字母组合</h2>
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

    示例:

    输入："23"
    输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

#### 方法一、递归

```javascript
var letterCombinations = function (digits) {
  if (digits == '') return []
  // 递归
  const map = {
    2: ['a', 'b', 'c'],
    3: ['d', 'e', 'f'],
    4: ['g', 'h', 'i'],
    5: ['j', 'k', 'l'],
    6: ['m', 'n', 'o'],
    7: ['p', 'q', 'r', 's'],
    8: ['t', 'u', 'v'],
    9: ['w', 'x', 'y', 'z'],
  }
  const result = []
  const helper = function (level, str) {
    // terminator
    if (level > digits.length) return result.push(str)
    // process current logic
    const f = digits[level - 1]
    for (let i of map[f]) {
      helper(level + 1, str + i)
    }
    // drill down
    // restore
  }
  helper(1, '')
  return result
};
```

#### 方法二，迭代 （Queue）

```javascript
var letterCombinations = function(digits) {
  if (digits.length == 0) return []
  const map = { 2: 'abc', 3: 'def', 4: 'ghi', 5: 'jkl', 6: 'mno', 7: 'pqrs', 8: 'tuv', 9: 'wxyz' }
  // 迭代， queue
  let level = 1
  const queue = [...map[digits[0]]]
  while (level < digits.length) {
    const n = queue.length
    for (let i = 0; i < n; i++) {
      const old = queue.shift()
      for (let c of map[digits[level]]) {
        queue.push(old + c)
      }
    }
    level++
  }
  return queue
};
```