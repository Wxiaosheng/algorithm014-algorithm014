> 学习 = 复习旧知识 + 学习新知识

## 复习昨日习题
不在单独提交 gitHub，直接在 leetCode 上重新答题，并且刷新提交记录

复习结果：
1. LeetCode 283 移动零， 比较熟练  
  一次循环，找零元素删除最后在补齐位数，或 使用双指针

2. LeetCode 70 爬楼梯， 熟练   
  递归 => 使用缓存 => 使用常数级的缓存

3. LeetCode 11 盛水最多容器，比较熟练
  暴力双层循环枚举所有情况 => 使用当层循环 + 双指针

4. LeetCode 15 三数之和，不太熟练(增加刷遍数)   
  两数之和，一层循环 + hash  
  三数之和，三层暴力循环，注意要去重   
  最优解法，排序 + 两层循环 + 双指针，同时要注意减支 + 去重

5. LeetCode 66 加一，熟练
  一层循环，只要没有发生进位，则直接 return，最后处理全都进位的情况

6. LeetCode 206 反转链表，不熟练(要刷)

> 最大的误区是，LeetCode 只刷一遍

## 刷题置顶🔝
1. [LeetCode 24 两两交换链表中的节点](#1)
2. [LeetCode 141 循环链表](#2)
3. [LeetCode 142 循环链表II - 入环节点](#3)

<h3 id="1">LeetCode 24 两两交换链表中的节点</h3>

本题自己没有很好的思路，第一次直接看的答案，官方给的有两种解法

#### 递归
* 递归其实正常的思维逻辑比较难以理解，通常来说，我们需要反向思考
* 例如这里，我们就需要先思考 [1, 2, 3, 4] 中 3 与 4 的交换
* 递归最重要的是 `终止条件`、`返回值`(某些特殊情况下，递归可能没有返回值)、`函数解决的重复子问题`
* `终止条件` - 链表为空 或 只有1个节点
* `函数解决的重复子问题` - 交换两个子节点
* `返回值` - 这里有，是交换后第一个节点的地址(其实就是原来第二个节点的地址，只是它的next指向发生了变化)

```js
// 递归解法
// 代码非常简洁，但是却难于理解
var swapPairs = function (head) {
  if (head === null || head.next === null) return head

  // 获取 第二个节点
  const next = head.next
  // 将节点交换后的结果放在第一个节点后
  head.next = swapPairs(next.next)
  // 将第二个节点的 next 指向第一个节点，完成位置交换
  next.next = head
  // 最后返回交换后 前一个节点
  return next
}
```

#### 非递归
一层循环，每次处理两个节点，注意：
1. 循环的更新条件是 **一次更新两个位置**
2. 要有一个虚拟的头结点，来存放第一次交换后，且要返回的新链表的头结点

```js
var swapPairs = function (head) {
  const vHead = new ListNode()
  vHead.next = head
  const temp = vHead
  while (temp.next !== null && temp.next.next !== null) {
    const start = temp.next
    const end = temp.next.next

    // 交换节点
    temp.next = end
    start.next = end.next
    end.next = start
    
    // 跟新循环变量
    temp = start
  }
}
```

<h3 id="2">LeetCode 141 环形链表</h3>

#### 自己想出来的方法，标记法
但是会改变原有的数据，不是很友好

```js
var hasCycle = function (head) {
  if (head === null || head.next === null) return false

  while (head) {
    if (head.isVisited) {
      return true
    }
    head.isVisited = true
    head = head.next
  }
  return false
}
```

#### 自己想出来的，使用 hash 存储访问记录，不在影响原有数据
```js
var hasCycle = function (head) {
  if (head === null || head.next === null) return false

  const hashSet = new Set()
  while (head) {
    if (hashSet.has(head)) {
      return true
    }
    hashSet.add(head)
    head = head.next
  }
  return false
}
```

#### 第三种方式，双指针 => 快慢指针
```js
var hasCycle = function (head) {
  if (head === null || head.next === null)  return false

  let fast = head, slow = head
  while (fast !== null && fast.next !== null) {
    slow = slow.next
    fast = fast.next.next
    if (fast === slow) {
      return true
    }
  }
  return false
}
```

<h3 id="3">LeetCode 142 循环链表II</h3>
即，判断有环链表的入环节点

#### 方法一，loop + hash，第一次重复出现的节点即为 入环节点，自己想出来的(秒出)

```js
var detectCycle = function (head) {
  if (head === null || head.next === null) return null

  const hashSet = new Set()
  while (head) {
    if (hashSet.has(head)) {
      return head
    }
    hashSet.add(head)
    head = head.next
  }
  return null
}
```

#### 方法二，其实是一种数学方法，通过现有公式推导出来的
假设，`头结点` 到 `入环节点` 的距离为 x，`入环节点` 到 `相遇节点` 的距离为 y，从 `相遇节点` 再到 `入环节点` 的距离为 z，即环的长度为 y + z  

当节点相遇时，fast 指针跑的是 slow 指针的两倍，因此 2 * (x + y) = x + y + n * (y + z)，其中 n 表示是跑了几圈

因此我们可以得到 x = n * (y + z) - y = (n - 1) * (y + z) + z，而 y + z 表示跑了一整圈，因此其实还是在相遇点，这就意味 x = z，即 **将其中一个指针指回原点，然后每次都走1步，再次相遇的节点即为 入环节点**

```js
var delectCycle = function (head) {
  if (head === null || head.next === null) return null

  const vHead = head
  let fast = head, slow = head
  while (fast !== null && fast.next !== null) {
    fast = fast.next.next
    slow = slow.next
    if (fast === slow) {
      // 有环
      break;
    }
  }
  if (fast !== slow) return null

  // 从开始，再次相遇的节点即为 入环节点
  fast = vHead
  while (fast !== slow) {
    fast = fast.next
    slow = slow.next
  }
  return fast
}
```