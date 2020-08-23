<h2 id="1">LeetCode 263 丑数</h2>
编写一个程序判断给定的数是否为丑数。  
丑数就是只包含质因数 2, 3, 5 的正整数。  

    示例 1:
      输入: 6
      输出: true
      解释: 6 = 2 × 3

    示例 2:
      输入: 8
      输出: true
      解释: 8 = 2 × 2 × 2

    示例 3:
      输入: 14
      输出: false 
      解释: 14 不是丑数，因为它包含了另外一个质因数 7。

说明：
1 是丑数。  
输入不会超过 32 位有符号整数的范围: [−231,  231 − 1]。  

** 总体的思路： 不断整除2，3，5，直到不能整除为止，判断整除后的数是否为1**

### 方法一、循环 + 依次判断当前的数，能否被  2、 3、5 整除

```javascript
var isUgly = function (n) {
  if (n <= 0) return false

  while (num >= 5) {
    if (num % 2 == 0) {
      num = num / 2
    }else if (num % 3 == 0) {
      num = num / 3
    } else if (num % 5 == 0) {
      num = num / 5
    } else {
      return false
    }
  }
  return num === 1
}
```

### 方法二、对于这种连续的 if -else if 的优化

```javascript
var isUgly = function (n) {
  if (n <= 0) return false
  const zs = [2, 3, 5]
  for (let i of zs) {
    while (num % i) {
      num = num / i
    }
  }
  return num === 1
}
```

