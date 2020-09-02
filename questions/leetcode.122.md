## LeetCode 122 买卖股票的最佳时机
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。  
设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。  
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。  

示例 1:  

    输入: [7,1,5,3,6,4]
    输出: 7
    解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
        随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。

示例 2:

    输入: [1,2,3,4,5]
    输出: 4
    解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
        注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
        因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
      
示例 3:

    输入: [7,6,4,3,1]
    输出: 0
    解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。

#### 方法一： recursion
> 方法是正确的，但是经过测试，发现超时

```javascript
var maxProfit = function (prices) {
  if (prices.length < 2) return 0

  let max = 0
  const helper = function (level, sum, buy) {
    // terminator
    if (level >= prices.length) return max = Math.max(max, sum)
    // process current logic
    // 买入
    if (buy.length < 1) helper(level + 1, sum, [prices[level]])
    if (buy.length > 0) {
      // 减枝
      if (buy[buy.length - 1] >= prices[level]) return
      // 卖出
      helper(level + 1, sum + prices[level] - buy[buy.length - 1], [])
    }
    // 不操作
    helper(level + 1, sum, buy)
    // drill down
    // restore
  }
  helper(0, 0, [])
  return max
}
``` 

#### 方法二：贪心算法
> 在每一步做出当前最佳的选择，即总是得到局部最优的结果，寄希望这样的选择能导致全局的结果最优

从第 i 天（这里 i >= 1）开始，与第 i - 1 的股价进行比较，如果股价有上升（严格上升），就将升高的股价（ prices[i] - prices[i- 1] ）记入总利润，按照这种算法，得到的结果就是符合题意的最大利润

```javascript
var maxProfit = function (prices) {
  if (prices.length < 2>) return 0
  let max = 0
  for (let i = 1; i < prices.length; i++) {
    if (prices[i] > prices[i - 1]) {
      max += prices[i] - prices[i - 1]
    }
  }
  return max
}
```

#### 方法三： 动态规划（思想）
> 可以用贪心算法解决的问题，一般情况下都可以用动态规划

```javascript
var maxProfit = function (prices) {
  let profit_out = 0, profit_in = 0 - prices[0];
  let n = prices.length;
  for (let i = 1; i < n; i++) {
    profit_out = Math.max(profit_out, profit_in + prices[i]);
    profit_in = Math.max(profit_in, profit_out - prices[i]);
  }
  return profit_out;
};
```