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


<h2 id='2'>LeetCode 74 搜索二维矩阵</h2>
编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

每行中的整数从左到右按升序排列。  
每行的第一个整数大于前一行的最后一个整数。  


#### 方法一： sort + includes

```javascript
var searchMatrix = function (matrix, target) {
    return matrix.flat(2).includes(target)
}
```

#### 方法二： 二分法

```javascript
var searchMatrix = function(matrix, target) {
    if (matrix.length == 0) return false
    const m = matrix.length
    const n = matrix[0].length

    let left = 0, right = m*n - 1
    while (left <= right) {
        const mid = Math.floor((left + right) / 2)
        const mx = Math.floor(mid / n)
        const my = mid % n
        if (matrix[mx][my] == target) return true
        if (matrix[mx][my] > target) right = mid - 1
        else left = mid + 1
    }
    return false
};
```