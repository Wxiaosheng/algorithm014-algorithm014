<h2 id="1">LeetCode 62 不同路径</h2>

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

    示例 1:
      输入: m = 3, n = 2
      输出: 3
      解释:
      从左上角开始，总共有 3 条路径可以到达右下角。
      1. 向右 -> 向右 -> 向下
      2. 向右 -> 向下 -> 向右
      3. 向下 -> 向右 -> 向右

    示例 2:
      输入: m = 7, n = 3
      输出: 28

提示：
1. 1 <= m, n <= 100
2. 题目数据保证答案小于等于 2 * 10 ^ 9


#### 方法一： 动态规划

```javascript
var uniquePaths = function (m, n) {
  if (m == 0 || n == 0) return 0
  const dp = (new Array(m).fill(1).map(i => (new Array(n).fill(1))))
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
    }
  }
  return dp[m - 1][n - 1]
}
```

<h2 id="2">LeetCode 63 不同路径 II</h2>
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 1 和 0 来表示。

说明：m 和 n 的值均不超过 100。

```javascript
var uniquePathsWithObstacles = function (obstacleGrid) {
  if (obstacleGrid.length == 0 || obstacleGrid[0].length == 0) return 0

  const m = obstacleGrid.length, n = obstacleGrid[0].length
  const dp = (new Array(m)).fill(1).map(i => (new Array(n)).fill(1))

  for (let i = 0; i < m; i++) {
    dp[i][0] = obstacleGrid[i][0] === 1 ? 0 : i - 1 > -1 ? dp[i - 1][0] : 1 
  }
  for (let j = 0; j < n; j++) {
    dp[0][j] = obstacleGrid[0][j] === 1 ? 0 : j - 1 > -1 ? dp[0][j - 1] : 1 
  }
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      dp[i][j] = obstacleGrid[i][j] === 1 ? 0 :( dp[i - 1][j] + dp[i][j - 1])
    }
  }
  return dp[m - 1][n - 1]
}
```


<h2 id="3">LeetCode 1143 最长公共子序列</h2>
给定两个字符串 text1 和 text2，返回这两个字符串的最长公共子序列的长度。

一个字符串的 子序列 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。
例如，"ace" 是 "abcde" 的子序列，但 "aec" 不是 "abcde" 的子序列。两个字符串的「公共子序列」是这两个字符串所共同拥有的子序列。

若这两个字符串没有公共子序列，则返回 0。


#### 方法一：Dynamic Programming

**将两个字符串按行和列进行排列，如果两个字符串相同位置的字符相同，则取前一行前一列的结果 + 1，否则取 前一行 或 前一列的 最大值**

```javascript
var longestCommonSubsequence = function (text1, text2) {
  const m = text1.length, n = text2.length
  if (m == 0 || n == 0) return 0
  const dp = (new Array(m + 1)).fill(0).map(i => (new Array(n + 1)).fill(0))
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      dp[i][j] = text1[i - 1] === text2[j - 1] ?
          (dp[i - 1][j - 1] + 1)
        :
          Math.max(dp[i - 1][j], dp[i][j - 1])
    }
  }
  return dp[m][n]
}
```
