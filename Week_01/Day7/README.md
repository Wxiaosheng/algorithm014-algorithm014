## 刷题置顶🔝

1. [Day6 LeetCode 42 接雨水](#1)

#### 方法二，暴力循环，按照每层的方式
这种解法和第一种比较类似，但是 会超出时间限制

```javascript
var trap = function(height) {
  if (height.length < 2) return 0
  let area = 0
  let rows = new Array(Math.max(...height) + 1).fill(0).map((v, i) => i)
  for (let i = 0; i < rows.length; i++) {
    let left = 0, right = height.length - 1
    // 找左边界
    while (height[left] - rows[i] <= 0) left++;
    // 找右边界
    while (height[right] - rows[i] <= 0) right--;
    for (let j = left; j <= right; j++) {
        if (height[j] - rows[i] <= 0) area++
    }
  }
  return area
}
```

