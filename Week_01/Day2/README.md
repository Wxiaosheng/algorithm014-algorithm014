> 学习 = 复习旧知识 + 学习新知识

## 复习昨日习题
1. [移动零](#1)

2. [盛水最多的容器](#2)

3. [爬楼梯](#3)

## 置顶(🔝)：实战题列表
1. [三数之和](#4)

2. [反转链表](#5)


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

<h3 id="4">三数之和</h3>
这道题个人只能写出三层循环 和 双层循环 + hash 的方式，但是都不能通过，提示 **超出时间限制**

```js
// 三层循环暴力求解
var threeSum = function (nums) {
  const result = []
  const hash = {}

  for (let i = 0; i < nums.length - 2; i++) {
    for (let j = i + 1; j < nums.length - 1; j++) {
      for (let k = j + 1; k < nums.length; k++) {
        if (nums[i] + nums[j] + nums[k] === 0) {
          const cur = [nums[i], nums[j], nums[k]]
          if (!hash[cur.toString()]){
            result.push(cur)
            hash[cur.toSting()] = true
          }
        }
      }
    }
  }
  return result
}
```

```js
// 两层循环
for (let i = 0; i < nums.length - 2; i++) {
  for (let j = i + 1; j < nums.length - 1; j++) {
    // 存在符合的元素
    if (hash[nums[j]] !== undefined) {
      result.push(nums[j].concat(hash[j]))
      hash[j] = undefined
    } else {
      const diff = 0 - nums[i] - nums[j]
      hash[diff] = [nums[i], nums[j]]
    }
  }
}
// 注意，此时的结果并没去重，因此最后要对结果做一个过滤
```

最后来看看，本题的最佳解法，
1. 先对数组去重
2. 使用双层循环，外层遍历每个元素
3. 内层循环，使用左右双指针，从当前元素后一位开始至最后一位，向所剩空间中间逼近

```js
var threeSum = function (nums) {
  const result = []

  // 排序
  nums = nums.sort((a, b) => a - b)

  for (let i = 0; i < nums.length; i++) {
    // 最下的数都大于0，则直接退出循环
    if (nums[i] > 0) break;

    // 去重
    if (i > 0 && nums[i] === nums[i - 1]) continue;

    let left = i + 1
    let right = nums.length - 1

    while (left < right)  {
      const cur = nums[i] + nums[left] + nums[right]
      if (cur === 0) {
        result.push([nums[i], nums[left], nums[right]])
        // 去重
        while (left < right && nums[left] === nums[left + 1]) continue;
        while (left < right && nums[right] === nums[right - 1]) continue;
        left++
        right--
      }
      if (cur < 0) {
        left++
      }
      if (cur > 0) {
        right--
      }
    }
  }
  return result
}
```


<h3 id="5">反转链表</h3>
自己使用以下两种方式写出来

```js
// 2次 loop，时间复杂度，空间复杂都高
var reverseList = function (head) {
  if (head === null || head.next === null) {
    return head
  }

  const arr = []
  while (head) {
    arr.push(head.val)
    head = head.next
  }

  let node = null
  let temp = null
  for (let i = arr.length - 1; i >= 0; i--) {
    if (node === null) {
      node = new ListNode(arr[i])
      temp = node
    } else {
      temp.next = new ListNode(arr[i])
      temp = temp.next
    }
  }
  return node
}
```
初次解出题目后，看到2次loop，因此对其进行优化，变成一次loop

使用一次loop的方法是这么实现的，循环到每个节点的时候，都声称新的结点，并且指向上一次循环创建的结点，因此需要一个单独的变量存储上一次累计创建的结点

```js
var reverseList = function (head) {
  if (head === null || head.next === null) return head

  let list = null
  while (head) {
    const node = new ListNode(head.val)
    node.next = list
    list = node
    head = head.next
  }
  return list
}
```

官方给出了两种解法，都不是太好理解，下面来看一下

```js
// 官方解法一
// 使用两个变量，分别存储当前结点的前一个结点，以及当前结点的 next
var reverseList = function (head) {
  if (head === null || head.next === null) return head;

  let pre = null
  let next = head
  while (next) {
    const temp = head.next
    head.next = pre
    pre = head
    next = temp
  }
  return pre
}

// 官方解法二，递归
// 正常思维非常不好理解，主要是因为递归程序是反向执行的

var reverseList = function (head) {
  if (head === null || head.next === null) return head;

  const p = reverseList(head.next)
  // 最后一次拿到的 p 是最后一个结点
  // 最后一次拿到的 head 是 p 的前节点
  head.next.next = head
  head.next = null
  return p
}
```