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


#### 方法一，迭代

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