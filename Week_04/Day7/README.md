<h2 id='1'>LeetCode 153 寻找旋转排序数组中的最小值</h2>
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

#### 方法一： loop - O(N)

#### 方法二： 二分查找
旋转排序数组 与 排序数组的却别：
* 相同点：
    * 都可以直接套用 二分法代码模板
* 不同点
    * 排序数组的二分法判断条件是 mid 与 target 比较
    * 旋转排序数组的二分法判断条件是 mid 与 right 比较，确定最小值可能存在的位置

```javascript
var findMin = function (nums) {
    let left = 0, right = nums.length - 1

    while (left < right) {
        const mid = Math.floor((left + right) / 2)
        if (nums[mid] < nums[right]) right = mid
        else left = mid + 1
    }
    return nums[left]
}
```