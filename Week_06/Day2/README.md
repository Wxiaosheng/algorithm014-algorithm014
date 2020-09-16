<h2 id="1">LeetCode 120 三角形最小路径和</h2>
给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

相邻的结点 在这里指的是 下标 与 上一层结点下标 相同或者等于 上一层结点下标 + 1 的两个结点。

    例如，给定三角形：

    [
           [2],
          [3,4],
         [6,5,7],
        [4,1,8,3]
    ]
    自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。

说明：如果你可以只使用 O(n) 的额外空间（n 为三角形的总行数）来解决这个问题，那么你的算法会很加分。

#### 方法一： recursion
> 解法效率不高，直接超时

```javascript
var minimumTotal = function (triangle) {
    if (triangle.length == 0) return 0

    const helper = function (i, j, sum) {
        // terminator
        if (i >= triangle.length) return sum
        // process current logic
        const left = helper(i + 1, j, sum)
        const right = helper(i + 1, j + 1, sum)
        // drill down
        // restore
        return Math.min(left, right) + triangle[i][j]
    }
    
    return helper(0, 0, 0)
}
```

#### 方法二： Dynamic Programming
> bottom-top， 自底向上，推导

```javascript
var minimumTotal = function (triangle) {
    if (triangle.length == 0) return 0
    const n = triangle.length, dp = (new Array(n)).fill([])
    dp[n - 1] = [...triangle[n - 1]]
    for (let i = n - 2; i >= 0; i--) {
        for (let i j = 0; j < triangle[i].length; j++) {
            dp[i][j] = Math.min(dp[i + 1][j], dp[i + 1][j + 1]) + triangle[i][j]
        }
    }
    return dp[0][0]
}
```

#### 方法三： 优化DP，只使用 O(n) 的额外空间

```javascript
var minimumTotal = function (triangle) {
    if (triangle.length == 0) return 0
    const n = triangle.length, dp = [...triangle[n - 1]]
    for (let i = n - 2; i >= 0; i--) {
        for (let j = 0; j < triangle[i].length; j++) {
            dp[j] = Math.min(dp[j], dp[j + 1]) + triangle[i][j]
        }
    }
    return dp[0]
}
```

<h2 id="2">LeetCode 198 打家劫舍</h2>
你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。

提示：
1. 0 <= nums.length <= 100
2. 0 <= nums[i] <= 400

#### 方法一： recursion
> DP 与 Recursion 没有本质的区别

**`Recursion` 会超时**

```javascript
var rob = function (nums) {
    if (nums.length == 0) return 0
    let max = 0
    const helper = function (level, sum) {
        // terminator
        if (level >= nums.length) return max = Math.max(max, sum)
        // process current logic
        helper(level + 1, sum)
        helper(level + 2, sum + nums[level])
        // drill down
        // restore
    }
    helper(0, 0)
    return max
}
```

#### 方法二： 动态规划
1. 最优子结构
    f(n) = max(f(n - 1), (f(n - 2) + n))
2. 中间结果
    dp[n]
3. 递推公式
    dp[n] = Math.max(dp[n-1], (dp[n-2] + n))

```javascript
var rob = function (nums) {
    const n = nums.length
    if (n == 0) return 0
    if (n < 3) return Math.max(...nums)

    const dp = [nums[0], Math.max(nums[0], nums[1])]

    for (let i = 2; i < n; i++) {
        dp[i] = Math.max(dp[i-1], (dp[i-2] + nums[i]))
    }
    return dp[n - 1]
}
```