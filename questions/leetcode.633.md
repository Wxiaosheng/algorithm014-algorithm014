## 平方数之和
给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a2 + b2 = c 。

示例 1：
输入：c = 5
输出：true
解释：1 * 1 + 2 * 2 = 5

    示例 ：
      输入：c = 3
      输出：false

      输入：c = 4
      输出：true

      输入：c = 2
      输出：true

      输入：c = 1
      输出：true
 
提示： 0 <= c <= 231 - 1

#### 方法一： loop + hash map
参考两数之和的思路

```javascript
var judgeSquareSum = function (c) {
  const hash = {}
  for (let n = 0; n * n < c; n++) {
    const curr = n * n
    if (hash[curr] || 2 * curr == c) return true
    hash[c - curr] = true
  }
  return false
}
```

#### 方法二：loop + 二分查找
对于当前的 a 来说，在 0 => c - a * a 中 找到 b * b = c - a * a

```javascript
var bs = function (n) {
  let left = 0, right = n
  while (left < right) {
    const mid = Math.floor((left + right) / 2), curr = mid * mid
    if (curr == n) return true
    if (curr < n) left = mid + 1
    else right = mid - 1
  }
  return left == right && left * left == n
}
var judgeSquareSum = function (c) {
  if (c < 3) return true
  for (let a = 0; a * a < c; a++) {
    if (bs(c - a * a)) return true
  }
  return false
}
```
