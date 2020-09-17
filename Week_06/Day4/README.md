<h2 id='1'>LeetCode 64 最小路径和 </h2>
给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。

        示例:
        输入:
        [
            [1,3,1],
            [1,5,1],
            [4,2,1]
        ]
        输出: 7
        解释: 因为路径 1→3→1→1→1 的总和最小。

#### 方法一：Dynamic Programming

1. 最有子结构： f[i][j] = min(f[i-1][j], f[i][j-1]) + curr
2. 中间状态： f[i][j]
3. 递推公式： dp[i][j] = dp[i-1][j] + dp[i][j-1]

```javascript
var minPathSum = function (grid) {
    if (grid.length == 0 || grid[0].lnegth == 0) return 0
    const m = grid.length, n = grid[0].length
    const dp = (new Array(m)).fill(0).map((v, i) => [...grid[i]])
    for (let i = 1; i < m; i++) {
        dp[i][0] = dp[i-1][0] + grid[i][0]
    }
    for (let j = 1; j < n; j++) {
        dp[0][j] = dp[0][j-1] + grid[0][j]
    }
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + grid[i][j]
        }
    }
    return dp[m-1][n-1]
}
```

