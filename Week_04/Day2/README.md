<h2 id='1'>LeetCode 69 x 的平方根</h2>
实现 int sqrt(int x) 函数。
计算并返回 x 的平方根，其中 x 是非负整数。
由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

    示例 1:
    输入: 4
    输出: 2

    示例 2:
    输入: 8
    输出: 2
    说明: 8 的平方根是 2.82842..., 
        由于返回类型是整数，小数部分将被舍去。

#### 方法一： Math 
```javascript
var mySqrt = function (x) {
  // √x => x ^ 1/2
  return Math.floor(Math.pow(x, 1/2))
}
```

#### 方法二： 二分查找
```javascript
var mySqrt = function (x) {
  if (x == 0 || x == 1) return x
  let left = 0, right = Math.floor(x / 2)
  while (left < right) {
    const mid = Math.floor((left + right) / 2 + 1)
    if (mid * mid > x) {
      right = mid - 1
    } else {
      left = mid
    }
  }
  return left
}
```

#### 方法三： 牛顿迭代法

```javascript
var mySqrt = function (x) {
  let a = x
  while (a * a > x) {
    a = Math.floor((a + x / a) / 2)
  }
  return a
}
```

<h2 id='2'>LeetCode 515 在每个树行中找最大值  </h2>
您需要在二叉树的每一行中找到最大的值。

示例：

    输入: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

输出: [1, 3, 9]

#### 方法一： BFS

```javascript
var largestValues = function(root) {
  if (root == null) return []

  const result = []
  const queue = [root]

  while (queue.length) {
    const n = queue.length
    let max
    for (let i = 0; i < n; i++) {
      const node = queue.shift()
      max = max === undefined ? node.val : Math.max(max, node.val)
      if (node.left) queue.push(node.left)
      if (node.right) queue.push(node.right)
    }
    result.push(max)
  }
  return result
};
```


#### 方法二：DFS + level

```javascript
var largestValues = function(root) {
  if (root == null) return []

  const result = []
  const helper = function (level, node) {
    // terminator
    if (node == null) return
    // process current logic
    result[level - 1] = result[level - 1] === undefined ? node.val : Math.max(result[level - 1], node.val)
    // drill down
    helper(level + 1, node.left)
    helper(level + 1, node.right)
    // restore
  }
  helper(1, root)
  return result
};
```

<h2 id='3'>LeetCode 367 有效的完全平方数</h2>
给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。
说明：不要使用任何内置的库函数，如  sqrt。

    示例 1：
      输入：16
      输出：True

    示例 2：
      输入：14
      输出：False

#### 方法一： 单层循环

```javascript
var isPerfectSquare = function (num) {
  if (num < 2) return num
  for (let i = 0; i <= num; i++) {
    if (i * i == num) return true 
  }
  return false
}
```

#### 方法二： 二分查找

```javascript
var isPerfectSquare = function (num)  {
  if (num < 2) return num

  let left = 1, right = num
  while (left <= right) {
    const mid = Math.floor((left + right) / 2) 
    const curr = mid * mid
    if (curr == num) return true
    if (curr > num) left = mid + 1
    if (curr < num) right = mid - 1
  }
  return false
}
```

#### 方法三、牛顿迭代法
```javascript
var isPerfectSquare = function (num) {
  if (num == 1) return num

  let mid = Math.floor(num / 2)
  while (!(mid * mid <= num && (mid + 1) * (mid + 1) > num)) {
    mid = Math.floor(mid - (mid * mid - num) / (2 * mid))
  }
  return mid * mid == num
}
```

#### 数学方法
```javascript
var isPerfectSquare = function (num) {
  let i = 1
  while (num > 0) {
    num -= i
    i += 2
  }
  return num == 0
}
```