## LeetCode 240 搜索二维矩阵

编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

每行的元素从左到右升序排列。  
每列的元素从上到下升序排列。

示例:

现有矩阵 matrix 如下：

    [
      [1,   4,  7, 11, 15],
      [2,   5,  8, 12, 19],
      [3,   6,  9, 16, 22],
      [10, 13, 14, 17, 24],
      [18, 21, 23, 26, 30]
    ]
给定 target = 5，返回 true。

给定 target = 20，返回 false。

#### 方法一： 系统API flat + includes
``` javascript
// Time Limit Exceeded
var  searchMatrix = function (matrix, target) {
  return matrix.flat(2).includes(target)
}
```

#### 方法二：暴力 循环
```javascript
var searchMatrix = function (matrix, target) {
  if (matrix.length == 0 || matrix[0].length == 0) return false
  const m = matrix.length, n = matrix[0].length
  for (let i = 0; i < m; i++) {
    // 减枝
    if (matrix[i][0] > target) return false;
    for (let j = 0; j < n; j++) {
      // 减枝
      if (matrix[i][j] > target) break;
      if (matrix[i][j] == target) return true
    }
  }
  return false
}
```

#### 方法三： 巧妙的二分法
从 `右上角` 的元素开始迭代：  
**1、 小于target，则取当前位置下一行的元素**  
**2、 大于target，则取当前位置前一列的元素**

```javascript
var searchMatrix = function (matrix, target) {
  if (matrix.length == 0 || matrix[0].length == 0) return false
  const m = matrix.length, n = matrix[0].length
  let row = 0, col = n - 1
  while (row < m && col >= 0) {
    const curr = matrix[row][col]
    if (curr == target) return true
    if (curr < target) row++
    else col--
  }
  return false
}
```