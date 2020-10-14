## LeetCode 191 位1的个数
编写一个函数，输入是一个无符号整数，返回其二进制表达式中数字位数为 ‘1’ 的个数（也被称为汉明重量）

      示例 1：
        输入：00000000000000000000000000001011
        输出：3
        解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。

      示例 3：
        输入：11111111111111111111111111111101
        输出：31
        解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。

#### 方法一： 特殊位运算
**清零最低位的1 => x = x & (x + 1)**

```javascript
var hammingWeight = function (n) { 
  let count = 0
  while (n != 0){
    n = n & (n + 1)
    count++
  }
  return count
}
```

## LeetCode 231 2的幂
给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

    示例:
      输入: 0
      输出: false

      输入: 1
      输出: true

      输入: 16
      输出: true

      输入: 218
      输出: false

#### 方法一： 特殊的位运算
* 除2：n / 2 => n >> 1
* 判断奇偶性： n % 2 => n & 1

```javascript
var isPowerOfTwo = function (n) {
  if (n == 0) return false
  if (n == 1) return true
  if (n & 1 == 1) return false
  return isPowerOfTwo(n >> 1)
}
```
