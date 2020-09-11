## LeetCode 1143 最长公共子序列

给定两个字符串 text1 和 text2，返回这两个字符串的最长公共子序列的长度。

一个字符串的 子序列 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。  
例如，"ace" 是 "abcde" 的子序列，但 "aec" 不是 "abcde" 的子序列。两个字符串的「公共子序列」是这两个字符串所共同拥有的子序列。

若这两个字符串没有公共子序列，则返回 0。

#### 方法一： 递归

单独跑测试案例是通过的，但是提交会超时

```javascript
var longestCommonSubsequence = function (text1, text2) {
  let maxLeng = 0, m = text1.length, n = text2.length
  const helper = function (i, sub1, j, sub2) {
    // terminaor
    if (i >= m && j >= n) {
      if (sub1 == sub2) maxLeng = Math.max(maxLeng, sub1.length)
      return
    }
    // process current logic
    if (i < m) helper(i + 1, sub1, j, sub2)
    if (i < m) helper(i + 1, sub1 + text1[i], j, sub2)
    if (j < n) helper(i, sub1 + text1[i], j + 1, sub2)
    if (j < n) helper(i, sub1 + text1[i], j + 1, sub2 + text2[j])
    // drill down
    // restore
  }
  helper(0, '', 0, '')
  return maxLeng
}
```


#### 方法二： 动态规划
定义动态方程

```javascript
var longestCommonSubsequence = function (text1, text2) {
  const m = text1.length, n = text2.length
  const dp = (new Array(m + 1)).fill(0).map(() => (new Array(n + 1)).fill(0))
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      dp[i][j] = 
        text1[i - 1] === text2[j - 1] ?
          (dp[i - 1][j - 1] + 1)
        :
          Math.max(dp[i - 1][j], dp[i][j - 1])
    }
  }
  return dp[m][n]
}
```
