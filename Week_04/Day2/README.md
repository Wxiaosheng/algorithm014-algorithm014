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
  if (x == 0) return 0
  let left = 0, right = Math.floor(x / 2)
  while (left < right) {
    const mid = Math.floor((left + right) / 2 + 1)
    if (mid * mid > x) {
      left = mid - 1
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

