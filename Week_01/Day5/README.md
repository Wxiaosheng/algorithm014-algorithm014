> 学习 = 复习旧知识 + 学习新知识

## 复习旧知识
> LeetCode 上再刷一遍

1. LeetCode 84 柱状图中最大的矩形 (比较熟练)

2. LeetCode 24 两两交换链表中的节点 (比较熟练，递归不好理解)

3. LeetCode 142 循环链表II - 入环节点 (不太熟练)
> 最爱犯的错误，将循环的终止条件放 与 循环条件的位置老是搞反

4. LeetCode 15 三数之和 (不熟练，继续刷)


## 刷题置顶🔝

1. [LeetCode 21 合并两个有序链表](#1)

2. [LeetCode 239 滑动窗口最大值](#2)

3. [LeetCode 26 删除排序数组中的重复项](#3)

4. [LeetCode 88 合并两个有序数组](#4)



<h3 id="1">LeetCode 21 合并两个有序链表</h3>

#### 方法一，循环遍历每个节点，每次确定一个节点的位置，但是需要一个单独的虚拟 头结点，存储新生成的节点

```JavaScript
var mergeTwoList = function (l1, l2) {
  if (l1 === null) return l2
  if (l2 === null) return l1

  const vHead = new ListNode()
  let temp = vHead
  while (l1 !== null && l2 !== null) {
    if (l1.val < l2.val) {
      temp.next = l1
      l1 = l1.next
    } else {
      temp.next = l2
      l2 = l2.next
    }
    temp = temp.next
  }
  return vHead.next
}
```


#### 方法二、递归，非常不利于理解，总觉得递归反人类思考方式，但是个人感觉应该是自己还没有掌握诀窍

**通常而言递归，都是从后往前执行的，和函数的执行顺序有点反过来的感觉**

##### 本题中，要特别注意一点，一次递归，只确定一个节点的顺序，会将第二个节点传到第二个递归函数中，因为大的节点，无法判断是否和小的节点直接来接

**本题现在是第二遍，但是还是很不熟练**

```javascript
var mergeList = function (l1, l2) {
  if (l1 === null) return l2
  if (l2 === null) return l1

  while (l1 !== null && l2 !== null) {
    if (l1.val <= l2.val) {
      l1.next = margeList(l1.next, l2)
      return l1
    } else {
      l2.next = mergeList(l1, l2.next)
      return l2
    }
  }
}
```




<h3 id="2">LeetCode 239 滑动窗口最大值</h3>

#### 方法一、使用一个 Queue 存储窗口的值，每次循环，取队列中的最大值

```javascript
var maxSlidingWindow = function (nums, k) {
  if (nums.length <= k) return [Math.max(...nums)]
  const queue = nums.slice(0, k)
  const result = [Math.max(...queue)]
  for (let i = k; i < nums.length; i++) {
    queue.shift()
    queue.push(nums[i])
    result.push(Math.max(...queue))
  }
  return result
}
```


#### 方法二、自定义滑动窗口类，始终让最大的值位于队列的最顶端，这样每次在获取最大值时，时间复杂度为 O(1)

```javascript
var maxSlidingWindow = function (nums, k) {
  if (nums.length <= k) return [Math.max(...nums)]
  class SliderWindow {
    constructor(){
      this.data = []
    }
    get length() {
      return this.data.length
    }
    push(v) {
      while (this.length > 0 && this.data[this.length - 1] < val) {
        this.data.pop()
      }
      this.data.push(v)
    }
    pop(v) {
      if (v === this.dta[0]) {
        this.data.pop()
      }
    }
    max(){
      return this.data[0]
    }
  }
  const result = []
  const sw = new SilderWindow()
  for (let i = 0; i < nums.length; i++) {
    if (i < k - 1) {
      sw.push(nums[i])
    } else {
      sw.push(nums[i])
      result.push(sw.max())
      sw.pop(nums[i - k + 1])
    }
  }
  return result
}
```


#### 第三种方法，动态规划规划， 没看懂(第一次看，没看懂)

```JavaScript
// 这份代码是 抄的
var maxSlidingWindow = function (nums, k) {
  if (nums.length <= k) return [Math.max(...nums)]

  let n = nums.length;
  let res = [];
  // 定义了两个队列
  let left = new Array(n), right = new Array(n);
  left[0] = nums[0];
  right[n - 1] = nums[n - 1];

  for (let i = 1; i < n; i++) {
    if (i % k == 0) left[i] = nums[i];
    else left[i] = Math.max(left[i - 1], nums[i]);
    let j = n - i - 1;
    if ((j + 1) % k == 0) right[j] = nums[j];
    else right[j] = Math.max(right[j + 1], nums[j]);
  }
  for (let i = 0; i < n - k + 1; i++) {
    res[i] = Math.max(left[i + k - 1], right[i]);
  }
  return res;
}
```

<h3 id="3">LeetCode 26 删除排序数组中的重复项</h3>

#### 方法，其实就是一个简单的双指针的方法，快慢指针

```javascript
var removeDuplicates = function (nums) {
  if (nums.length < 2 ) return nums.length

  let length = 0
  for (let i = 1; i < nums.length; i++) {
    if (nums[i] !== nums[length]) {
      nums[++length] = nums[i]
    }
  }
  return length + 1
}
```


<h3 id="4">LeetCode 88 合并两个有序数组</h3>

```javascript
var merge = function (num1, m, num2, n) {
  const sortArr = num1.slice(0, m).concat(num2.slice(0, n)).sort((a, b) => a - b)
  num1.splict(0, sortArr.length, ...sortArr)
  return num1
}
```
