## LeetCode 560 和为K的子数组
给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

示例 1 :  
  * 输入:nums = [1,1,1], k = 2  
  * 输出: 2 , [1,1] 与 [1,1] 为两种不同的情况  

说明 :
  1. 数组的长度为 [1, 20,000]。
  2. 数组中元素的范围是 [-1000, 1000] ，且整数 k 的范围是 [-1e7, 1e7]

#### 方法一： 暴力求解
从第一位开始，求解当前位及前面的和，与 k 比较

```javascript
var subArraySum = function (nums, k) {
  if (nums.length == 0) return 0
  let count = 0
  for (let i = 0; i < nums.length; i++) {
    let sum = 0
    for (let j = i; j >= 0; j--) {
      sum += num[j]
    }
    if (sum == k) count++
  }
  return count
}
```

#### 方法二： 在方法一的基础上，使用 hash 缓存之前计算的结果

```javascript
var subArraySum = function (nums, k) {
  if (nums.length == 0) return 0
  let preSum = 0, count = 0
  const map = { 0: 1 }
  for (let i = 0; i < nums.length; i++) {
    preSum += nums[i]
    if (map[preSum - k]) count += map[preSum - k]
    map[preSum] = map[preSum] === undefined ? 1 : map[preSum] + 1
  }
  return count
}
```