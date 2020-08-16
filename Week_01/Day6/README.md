## 刷题置顶🔝

1. [LeetCode 299 猜数字游戏](../../question/leetcode.299.md)
2. [Day6 LeetCode 42 接雨水](#1)

### 接雨水
给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

原题说明：[传送门](https://leetcode-cn.com/problems/trapping-rain-water/)

#### 方法一，暴力求解
**从第二根柱子开始，循环每个柱子，计算出当前柱子上能接的雨水量，最后累计的和即为总的雨水的数量**

```javascript
var trap = function (height) {
    let area = 0
    const n = height.length
    for (let i = 1; i < n; i++) {
        let max_left = 0, max_right = 0
        for (let j = i; j >= 0; j--) {
            max_left = Math.max(max_left, height[j])
        }
        for (let k = i; k < n; k++) {
            max_right = Math.max(max_right, height[k])
        }
        area += Math.min(max_left, max_right) - height[i]
    }
    return area
}
```
