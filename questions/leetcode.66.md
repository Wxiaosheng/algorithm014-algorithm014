## LeetCode 66. 加一
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。


### 方法一： 简单的loop
反向遍历 整个数组，最后一位加 1，判断是否出现进位的情况
```js
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function (digits) {
  const result = []
  const isUp = ture 
  for (let i = digits.length - 1; i >= 0; i--) {
    let num = isUp ? digits[i] + 1 : digits[i]
    if (num > 9) {
      result.unshift(0)
      isUp = true
      if (i === 0) {
        result.unshift(1)
      }
    } else {
      result.unshift(num)
      isUp = false
    }
  }
  return result
}
```
这种方法是自己想出来，但是不好，有两个方面可以优化：
1. 当没有进位发生时，无论是最后一位，还是中间的某一位，则改位数字前的所有数字其实都不可能发生进位了，因此可以直接返回前面的数据，而无需处理
2. 新开了一个数组，增加空间复杂度

### 方法二：最佳实践
```js
var plusOne1 = function (digits) {
  for (let i = digits.length - 1; i >= 0; i--) {
    digits[i]++
    digits[i] %= 10
    // 对于没有发生进位前的数字，可以直接返回
    if (digits[i] !== 0) {
      return digits
    }
  }
  // 如果循环结束还未返回，则每一位都发生了进位，因此需要在最前补充最高位
  digits.unshift(1)
  return digits
}
```
```js
// 另一种表现形式
var plusOne2 = function (digits) {
  for (let i = digits.length - 1; i >= 0; i--) {
    if (digits[i] === 9) {
      digits[i] = 0
    } else {
      digits[i]++
      return digits
    }
  }
  digits.unshift(1)
  return digits
}
```
注意： 相对来说，plusOne1 的代码行数更少，但是 个人感觉 plusOne2 的代码逻辑更符合人类思维，易于理解