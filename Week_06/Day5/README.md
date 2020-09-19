<h2 id="1">LeetCode 22 买卖股票的最佳时机 II</h2>
> Greedy, 复习

```javascript
var maxProfit = function (prices) {
  if (prices.length < 2) return 0
  let sum = 0
  for (let i = 1; i < prices.length; i++) {
    if (prices[i] > prices[i-1]) {
      sum += prices[i] - prices[i-1]
    }
  }
  return sum
}
```

<h2 id="2"></h2>