## LeetCode 213 打家劫舍 II

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