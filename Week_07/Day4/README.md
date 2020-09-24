<h2 id="1">LeetCode 547 朋友圈</h2>

班上有 N 名学生。其中有些人是朋友，有些则不是。他们的友谊具有是传递性。如果已知 A 是 B 的朋友，B 是 C 的朋友，那么我们可以认为 A 也是 C 的朋友。所谓的朋友圈，是指所有朋友的集合。

给定一个 N * N 的矩阵 M，表示班级中学生之间的朋友关系。如果M[i][j] = 1，表示已知第 i 个和 j 个学生互为朋友关系，否则为不知道。你必须输出所有学生中的已知的朋友圈总数。

 
    输入：
      [[1,1,0],
      [1,1,0],
      [0,0,1]]
    输出：2 
    解释：
      已知学生 0 和学生 1 互为朋友，他们在一个朋友圈。
      第2个学生自己在一个朋友圈。所以返回 2 。

    输入：
      [[1,1,0],
      [1,1,1],
      [0,1,1]]
    输出：1
    解释：
      已知学生 0 和学生 1 互为朋友，学生 1 和学生 2 互为朋友，所以学生 0 和学生 2 也是朋友，所以他们三个在一个朋友圈，返回 1 。
 
提示：
* 1 <= N <= 200
* M[i][i] == 1
* M[i][j] == M[j][i]

#### 方法一： Breadth First Search
```javascript
var findCircleNum = function (M) {
  if (M.length == 0 || M[0].length == 0) return 0
  let count = 0
  const m = M.length, n = M[0].length, visited = new Set()

  var bfs = function (n) {
    for (let j = 0; j < n; j++) {
      if (M[n][j] == 1 && !visited.has(j)) {
        visited.add(j)
        bfs(j)
      }
    }
  }

  for (let i = 0; i < m; i++) {
    if (!visitd.has(i)) {
      bfs(i)
      count++
    }
  }
  return count
}
```

<h2 id="2">LeetCode 152 乘积最大子序列</h2>
给你一个整数数组 nums ，请你找出数组中乘积最大的连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

    示例 1:
      输入: [2,3,-2,4]
      输出: 6
      解释: 子数组 [2,3] 有最大乘积 6。

    示例 2:
      输入: [-2,0,-1]
      输出: 0
      解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。

#### 方法一： Dynamic Programming
> 注意与 LeetCode 53 最大子序和 

```javascript
var maxProduct = function (nums) {
  let min = 1, max = 1, result = nums[0]

  for (let n of nums) {
    if (n < 0) [min, max] = [max, min]
    min = Math.min(n, n * min)
    max = Math.max(n, n * max)
    result = Math.max(max, result)
  }
  return result
}
```