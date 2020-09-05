<h2 id='1'>LeetCode 33 搜索旋转排序数组</h2>
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

#### 方法一： 一遍循环 - O(N)
> 不符合题目要求

#### 方法二： 使用系统函数

```javascript
var search = function (nums, target) {
    return nums.indexOf(target)
}
```

#### 方法三：二分查找
> 前提：有序、确定边界、可直接访问

```javascript
var search = function (nums, target) {
    let left = 0, right = nums.length
    while (left < right) {
        const mid = Math.floor((left + right) / 2)
        // [0, mid] 有序，且 target 不在其中
        if (nums[0] <= nums[mid] && (target > nums[mid] || target < nums[0])) {
            left = mid + 1
        // [0, mid] 无序，且 target 不在其中 
        } else if (target < nums[0] && target > nums[mid]) {
            left = mid + 1
        } else {
            right = mid
        }
    }
    return left == right && nums[left] == target ? left : -1
}
```

