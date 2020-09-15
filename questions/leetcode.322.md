## LeetCode 322 零钱兑换
给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

    示例 1:
    输入: coins = [1, 2, 5], amount = 11
    输出: 3 
    解释: 11 = 5 + 5 + 1

    示例 2:
    输入: coins = [2], amount = 3
    输出: -1
 
说明: 你可以认为每种硬币的数量是无限的。

#### 方法一： Dynamic Programming

```javascript
var coinChange = function (coins, amount) {
  // 1. 寻找 最优子结构 （optional constructure）
  // 2. 存储中间状态 dp[i]
  // 3. 递推公式 dp[n] = min(dp[i - coins1], dp[i - coins2], ...) + 1
  if (coins.length == 0) return -1
  const dp = new Array(amount + 1)
  for (let i = 1; i <= amount; i++) {
    let min = Number.MAX_VALUE
    for (let j = 0; j < coins.length; j++) {
      if (i - coins[j] >= 0 && min > dp[i - coins[j]]) 
        min = Math.min(min, dp[i - coins[j]]) + 1;
    }
    dp[i] = min
  }
  return dp[amount] === Number.MAX_VALUE ? -1 : dp[amount]
}
```