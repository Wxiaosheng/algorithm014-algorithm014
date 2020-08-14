> 学习 = 复习旧知识 + 学习新知识

## 复习旧知识
> LeetCode 上再刷一遍

1. LeetCode 206 反转链表 (熟练)

2. LeetCode 24 两两交换链表中的节点 (不熟练，递归不好理解)

3. LeetCode 141 循环链表 (熟练)

4. LeetCode 142 循环链表II - 入环节点 (不熟练)

5. LeetCode 15 三数之和 (不太熟练)

## 刷题制定
1. [LeetCode 20 有效的括号]()

## 学习新知识
### 第4课，栈、队列、优先队列、双端队列

#### Stack - 栈
First In Last Out

#### Queue - 队列
First In First Out


#### Deque: Double-end Queue - 双端队列


#### Priority Queue - 优先队列
1. 插入操作 O(1)

2. 取出操作 O(logn)，按照元素优先级取出

3. 具体底层实现的数据结构较为多样和复杂： heap、bst、treap

#### 作业
1. priority queue 源代码分析


## 第四课，实战题目解析：有效的括号、最小栈等问题

<h3 id="1">LeetCode 20 有效的括号</h3>
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：
1. 左括号必须用相同类型的右括号闭合
2. 左括号必须以正确的顺序闭合
3. 注意空字符串可被认为是有效字符串

其实在判断左括号是否与右括号配对时，第一次出现的左括号是最后一次才匹配。最后出现的左括号，确实最先开始匹配的  

**因此我们尝试使用 Stack 的数据结构来实现**

```js
var isValid = function (s) {
    // 基数位 肯定不会匹配
    if (s.length % 2 === 1) return false

    // 借助 hash，快速判断左右括号是否匹配
    const hash = {
        ')': '(',
        ']': '[',
        '}': '{',
    }
    const stack = []
    for (let i = 0; i < s.length; i++) {
        if (s[i] === '(' || s[i] === '[' || s[i] === '{') {
            stack.push(s[i])
        } else {
            if (hash[s[i]] !== stack.pop()) {
                return false
            }
        }
    }
    // 空栈才表示 合法
    return stack.length === 0
}
```

<h3 id="2">LeetCode 84 柱状图中最大的矩形</h3>
给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。


### 为什么可以想到用 栈 或 队列 来解决？
其实程序都是人类思考的产物，往往一个东西并不是凭空的的发明创造出来的，而是根据现实生活中的我们常见的事物创建出来的  

栈，其实类似于像 洋葱、子弹夹等那样，后进先出的，但是往往在程序中并不是一条路走到黑，满足某种情况下才会入栈，然后满足另一种情况就会出栈，然后交替执行，这样总体看起来和 先进后出并不是完全吻合，但是在处理相似的子问题时，一定是先进后出的

队列，也是同样的，就像生活中排队购物一样，讲究的是先来后到，计算机处理的最基础的单元其实就是最简单的逻辑单元，正好需要这种模式

#### 方法一，暴力枚举所有情况
```js
var largestRectangleArea = function(heights) {
  // 方法一，暴力法
  if (heights.length === 0) return 0
  if (heights.length === 1) return heights[0]

  let area = 0
  for (let i = 0; i < heights.length; i++) {
    // 初始化当前循环中，最小的高度
    let minHeight = heights[i]
    for (let j = i; j < heights.length; j++) {
      minHeight = Math.min(minHeight, heights[j])
      area = Math.max(area, (j - i + 1) * minHeight)
    }
  }
  return area
};
```


#### 方法二，枚举每一个高度，计算对应高度矩形的面积
```js
var largestRectangleArea = function(heights) {
    if (heights.length === 0) return 0

    let area = 0
    for (let i = 0; i < height.length; i++) {
        const curHeight = height[i]

        let left = i
        let right = i

        // 左边界，小于当前高度的 高度
        while (left > -1 && height[left] >= curHeight) left--
        // 右边界，小于当前高度的 高度
        while (right < height.length && height[right] >= curHieght) right++

        area = Math.max(area, (right - left - 1) * curHeight)
    }
    return area
}
```

#### 方法三，一层循环 + maxStack
```js
var largestRectangleArea = function(heights) {
    if (heights.length === 0) return 0

    let area = 0
    const maxStack  = []
    // 保证能在一次循环后，栈为空
    heights = [0, ...heights, 0]
    for (let i = 0; i < heights.length; i ++) {
        const curHeight = heights[i]
        while (curHeight < maxStack[maxStack.length - 1]) {
            const stackTop = maxStack.pop()
            // 面积为 当前下标与 出栈后栈顶元素的下标之差 - 1
            area = Math.max(area, (i - maxStack[maxStack.length - 1] - 1) * curHeight)
        }
        maxStack.push(i)
    }
    return area
}
```
