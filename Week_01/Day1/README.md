给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

说明:
1. 必须在原数组上操作，不能拷贝额外的数组。
2. 尽量减少操作次数。

```js
// 如果不考虑限制条件，其实可以使用系统API
// 将非零元素 与 零元素分别过滤出来，拼接在一起即可
var moveZeroes = function (nums) {
  return nums.filter(num => num !== 0).concat(nums.filter(num => num === 0))
}
```

```js
// 在不修改元素，并且保持非零元素的相对位置 条件下
// 循环数组，将零元素 与 该元素后的第一个非零元素交换位置

var moveZeroes = function (nums) {
  if (nums.length < 2) {
    return nums
  }

  for (let i = 0; i < nums.length; i++) {
    if (nums[i] === 0) {
      for (let j = i + 1; j < nums.length; j++) {
        if (nums[j] !== 0) {
          nums[i] = nums[j]
          nums[j] = 0
          break;
        }
      }
    }
  }
  return nums
}
```
这种方法不好，时间复杂度为 O(n^2)，还有优化的空间，常见的优化思想有 **升维思想** 和 **空间换时间**  

```js
// 这里我们使用类似 升维思想，在一层 loop 中使用双指针
// 此时 算法的时间复杂度即为 O(n)

var moveZeroes = function (nums) {
  if (nums.length < 2) {
    return nums
  }

  let j = 0; // 非零元素的下标
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== 0) {
      nums[j] = nums[i]
      if (i !== j) {
        nums[i] = 0
      }
      j++
    }
    /*
      这里见到一种更少的代码的写法，代码行数少，但是总感觉不符合正常思考的逻辑
      if (nums[i] !== 0) {
        const temp = nums[i]
        nums[i] = nums[j]
        nums[j++] = temp
      }
    */
  }

  return nums
}
```

这道题的解法，通过观看大牛的各种解题思路可以发现，loop的时候，可以找非零元素交换位置，也可以找零元素，删除在添加

```js
// 这里最好要使用倒叙，因为如果正序，则需要在删除零元素后纠正下标的位置
var moveZeroes = function (nums) {
  for (let i = nums.length; i >= 0; i--) {
    if (nums[i] === 0) {
      nums.splice(i, 1)
      nums.push(0)
    }
  }
  return nums
}
```
注意： 这种方法写起来很简单，但是其实效率并不好，因为我们都知道数组的 delete 的算法复杂度是 O(n)