## LeetCode 283 移动零

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

    示例:
    输入: [0,1,0,3,12]
    输出: [1,3,12,0,0]

说明:

  必须在原数组上操作，不能拷贝额外的数组。    
  尽量减少操作次数。  

### 方法一，两层暴力循环

### 方法二，针对线结构的两层遍历，通产可以优化成一层遍历 + 双指针

```javascript
var moveZero = function (nums) {
  if (nums.length < 2) return nums

  for (let i = 0, j = 0; i < nums.length; i++) {
    if (nums[i] !== 0) {
      nums[j] = nums[i]
      if (i !== j) nums[i] = 0
    }
  }
  return nums
}
```

### 方法三，找到非零元素删除， 数组尾部补 0
> 注意，此方法要从后往前遍历

```javascript
var moveZero = function (nums) {
  if (nums.length < 2) return nums

  for (let i = nums.length - 1; i >= 0; i--) {
    if (nums[i] == 0) {
      nums.splice(i, 1)
      nums.push(0)
    }
  }
  return nums
}
```

