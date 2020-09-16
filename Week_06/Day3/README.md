<h2 id="1">LeetCode 213 打家劫舍 II</h2>

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都围成一圈，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你在不触动警报装置的情况下，能够偷窃到的最高金额。

#### 方法一：Dynamic Programming

本题与 198 打家劫舍  的题目非常类似，只是新增的一个约束条件，房屋是环形， 因此不能偷到 第一间房 和 最后一间房

这样其实就转化为两个子问题了：
1. 偷第一间房，不可以偷最后一间房
2. 不偷第一件房，可以偷最后一间房

**取 二者的 较大值**

```javascript
var rob = function (nums) {
  if (nums.length == 0) return 0
  if (nums.length < 3) return Math.max(...nums)
  const hepler = function (nums) {
    const n  = nums.length
    if (n < 3) return Math.max(...nums)
    const dp = [nums[0], Math.max(nums[0], nums[1])]
    for (let i = 2; i < n; i++) {
      dp[i] = Math.max(dp[i - 1], (dp[i - 2] + nums[i]))
    }
    return dp[n - 1]
  }
  return Math.max(helper(nums.slice(0, nums.length  - 1), nums.slice(1)))
}
```

<h2 id="2">买卖股票的最佳时机</h2>
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。

注意：你不能在买入股票前卖出股票。

#### 方法一： 暴力 loop
循环每一天的股价，然后找出后面天数中的最大值，二者的差就是当前情况的最大值，然后更新最大值

```javascript 
// runtime => 5.5 % 
var maxProfit = function (prices) {
  if (prices.length < 2) return 0

  let max = 0
  for (let i = 0; i < prices.length - 1; i++) {
    const prev = prices[i]
     max = Math.max(max, Math.max(...(prices.slice(i + 1))) - prices[i])
  }
  return max
}
```

**由于操作数组很慢，因此直接使用 loop 来找到后续天数中的最大值**

```javascript
// runtime => 19.01 % 
var maxProfit = function (prices) {
  if (prices.length < 2) return 0
  let max = 0
  for (let i = 0; i < prices.length - 1; i++) {
    let subMax = prices[i + 1]
    for (let j = i + 1; j < prices.length; j++) {
      subMax = Math.max(subMax, prices[j])
    }
    max = Math.max(max, subMax - prices[i])
  }
  return max
}
```

#### 方法二： Dynamic Programming

在买卖股票时，我们都希望我们会在历史的最低点买入，因此我们可以使用一个变量min_price记住, 然后再用另一个变量 max 记录当前的最大利润

**自己在思考这个问题的时候，定义最佳子结构时，只能想到使用一个变量记录 最大利润，而想不到新增一个遍历来记录历史最低点，以后最优子节点定义不出来时，可以尝试新增变量，或者给一维数组升维**

```javascript
var maxProfit = function (prices) {
  if (prices.length < 2) return 0

  let min_price = prices[0], max = 0
  for (let i = 1; i < prices.length; i++) {
    if (prices[i] < min_price) {
      min_price = prices[i]
    } else {
      max = Math.max(max, prices[i] - min_price)
    }
  }
  return max
}
```