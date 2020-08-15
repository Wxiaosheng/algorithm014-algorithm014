## LeetCode 1. 两数之和
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。


### 解法一： 暴力循环，枚举所有可能的情况

```js
var towSum = function (nums, target) {
    if (nums.length < 2) return []
    if (nums.length === 2) {
        if (nums[0] + nums[1] === target) return [0, 1]
    }

    for (let i = 0; i < nums.length - 1; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] === target) {
                return [i, j]
            }
        }
    }
    return []
}
```

### 解法二，借助 hash 表，缓存数据，降低时间复杂度，不过同时增加了空间复杂度
```js
var twoSum = function(nums, target) {
    if (nums.length < 2) return []
    
    const hash = {}
    for (let i = 0; i < nums.length; i++) {
        if (hash[nums[i]] !== undefined) {
            return [hash[nums[i]], i]
        } 
        hash[target - nums[i]] = i
    }
    return []
}
```