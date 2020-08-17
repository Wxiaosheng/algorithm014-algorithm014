## LeetCode 350 两个数组的交集 II

给定两个数组，编写一个函数来计算它们的交集。

示例 1： 

  输入：nums1 = [1,2,2,1], nums2 = [2,2]  
  输出：[2,2]  

示例 2:  

  输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]  
  输出：[4,9]  


### 方法一：hashMap
1. 循环长的数组，记录数组中元素出现的次数
2. 循环短的数组，查询 hashMap 中是否存在，如果存在则为交集，计数并减一

```javascript 
var intersect = function (nums1, nums2) {
  const maxArr = nums1.length > num2.length ? nums1 : nums2
  const minArr = nums1.length <= num2.length ? nums1 : nums2
  const hashMap = {}
  const result = []
  for (let i = 0; i < maxArr.length; i++) {
    hashMap[maxArr[i]] = hashMap[maxArr[i]] ? hashMap[maxArr[i]] + 1 : 1
  }

  for (let i = 0; i < minArr.length; i++) {
    if (maxArr[i]] > 0) {
      resule.push(maxArr[i]])
      maxArr[i]]--
    }
  }
  return result
}
```

### 方法二，双指针法
> 因为 “我们可以不考虑输出结果的顺序”

1. 对两个数组排序
2. 定义两个指针，分别用于遍历两个数组
3. 如果相等，则为交集，两个指针同时向后移动一位
4. 如果不等，则移动较小的指针

```javascript
var intersect = function (nums1, nums2) {
  nums1 = nums1.sort((a, b) => a - b)
  nums2 = nums2.sort((a, b) => a - b)

  const result = []
  let i = 0, j = 0
  while (i < nums1.length && j < nums2.length) {
    if (nums1[i] === nums2[j]) {
      result.push(nums1[i])
      i++, j++
    }
    if (nums1[i] < nums2[j]) i++
    if (nums2[j] < nums1[i]) j++
  }
  return result
};
```

### 方法三，非常巧妙的办法
1. 遍历其中一个数组，在另一个数组中查找当前元素是否存在
2. 如果存在，则另一个数组删除该元素，并将该元素存进结果中

```javascript 
var intersect = function (nums1, nums2) {
  const result = []
  for (let i = 0; i < nums1.length; i++) {
    const index = nums2.indexOf(nums1[i])
    if (index > -1) {
      result.push(nums2.splice(index, 1)[0])
    }
  }
  return result
}
```
