<h2 id="1">LeetCode 16 最接近的三数之和</h2>
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

    示例：
      输入：nums = [-1,2,1,-4], target = 1
      输出：2
      解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
 
提示：
1. 3 <= nums.length <= 10^3
2. -10^3 <= nums[i] <= 10^3
3. -10^4 <= target <= 10^4

#### 方法一： 三数之和 思想
sort + loop  + 双指针

```javascript
var threeSumClosest = function (nums, target) {
  let sum = 0, min = Number.MAX_VALUE
  nums.sort((a, b) => a - b)
  for (let i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] == nums[i-1]) continue
    let left = i+1, right = nums.length -1
    const curr = nums[i] + nums[left] + nums[right]
    if (Math.abs(target - curr) < min) {
      sum = curr
      min = Math.abs(target - curr)
    }
    if (curr < target) left++
    else right--
  }
  return sum
}
```