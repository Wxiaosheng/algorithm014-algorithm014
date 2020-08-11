> 学习 = 复习旧知识 + 学习新知识

## 复习昨日习题
1. [移动零](#1)

2. [盛水最多的容器](#2)

3. [爬楼梯](#3)

## 置顶(🔝)：实战题列表


<h3 id="1">移动零</h3>
思路：

1. 方法一，双层循环遍历，外层循环找零元素，内层循环找非零元素
2. 方法二，使用双指针 （最佳方法）
    * 其实这个方法可以延伸成两种形式，找零元素或非零元素，进行删除操作或交换位置

```js
var moveZeroes = function(nums) {
  for (let i = 0, j = 0; i < nums.length; i++) {
    if (nums[i] !== 0) {
      nums[j] = nums[i]
      if ( i !== j) {
        nums[i] = 0
      }
      j++
    }
  }
  return nums
}
```

<h3 id="2">盛水最多的容器</h3>
思路：

1. 方法一，双层loop暴力求解，遍历所有可能组合情况并计算出响应的面积，记录最大值
2. 方法二，使用双指针，或者叫前后指针，从两端向中间不断夹逼的办法（最佳方法）

```js
var maxArea = function (height) {
  let area = 0
  for (let i = 0, j = height.length - 1; j > i; ) {
    const minHeight = height[i] <= height[j] ? height[i++] : height[j--]
    area = Math.max(area, (j - i) * minHeight)
  }
  return area
}
```


<h3 id="3">爬楼梯</h3>

思路：

1. 这一道题其实没有什么比较好的办法，刚开始拿到题的时候，没有什么思路，而且也不能通过暴力的求解的方式得出答案
    * 一般情况下，当我们面对一个题目懵逼时，该如何解决呢？
    * 由于计算机只是一种机器，其实它本身是无法做很复杂的事情的，只能处理 `if-else`、`loop`、`resursion` 等这样简单的操作
    * 因此，当我们没有思路时，不妨思考问题最最简单的情况（如只走一阶台阶），然后尝试找到重复的相类似的问题，往简答的编程语句上靠

2. 其实这道题是一个斐波那契数列的例子，使用递归即可解决
3. 但是使用递归的方式存在很大的重复计算的问题，算法复杂度达到了O(n^2)，因此我们对计算结果做缓存
4. 一般来说，做缓存则意味着要重新开辟存储空间，是一种空间换时间的思想，因此在此尝试降低空间复杂度，即可得到最优解

```js
var climbStaris = function (n) {
  let total = 1
  let preOne = 1
  let preTwo = 1
  if (n < 2) {
    return total
  }
  for (let i = 2; i <= n; i++) {
    total = preOne + preTwo
    preTwo = preOne
    preOne = total
  }
  return total
}
```


