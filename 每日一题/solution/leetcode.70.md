假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。


```js
// 自己的思路
// 这道题其实是一个斐波那契数列
// 即，f(n) = f(n-1) + f(n-2)

var climbStairs = function (n) {
  if (n < 1) {
    return 1
  }

  return climbStairs(n - 1) + climbStairs(n - 2)
}
```
这段代码本身其实是没有问题的，但是提交 LeetCode 之后，结果为 **超出时间限制**

原因就是，这个递归函数存在大量的重复的计算，因此当将计算的结果缓存起来，就能提高程序的执行效率

```js
// 优化后的解法 (将计算的结果都放在一个数组中)

var climbStairs = function (n) {
  const dp = []
  dp[0] = dp[1] = 1
  if (let i = 2; i <= n; i++) {
    dp[n] = dp[n - 1] + dp[n - 2]
  }
  return dp[n]
}
```
对于这种解法其实将已经降低时间复杂度为 O(n)，但是却增加了空间复杂度，在国际站上，最高票答案提供了一种既降低了时间复杂度，同时也不用牺牲空间的算法

```js
// 最佳答案

var climbStaris = function (n) {
  let preStepOne = 1
  let preStepTwo = 1
  let totalStep = 1

  if (n < 2) {
    return totalStep
  }

  for (let i = 2; i <= n; i++) {
    totalStep = preStepOne + preStepTwo
    preStepTwo = preStepOne
    preStepOne = totalStep
  }

  return totalStep
}
```


