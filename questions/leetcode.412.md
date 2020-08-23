## LeetCode 412 Fizz Buzz
写一个程序，输出从 1 到 n 数字的字符串表示。

1. 如果 n 是3的倍数，输出“Fizz”
2. 如果 n 是5的倍数，输出“Buzz”
3. 如果 n 同时是3和5的倍数，输出 “FizzBuzz”


### 方法一，loop + 判断

```javascript
var fizzBuzz = function (n) {
  if (n == 0) return []
  const result = []
  for (let i = 1; i <= n; i++) {
    if (i % 3 == 0 && i % 5 == 0) {
      result.push("FizzBuzz")
    } else if (i % 3 == 0) {
      result.push("Fizz")
    }
    } else if (i % 5 == 0) {
      result.push("Buzz")
    } else {
      result.push(i + '')
    }
  }
  return result
}
``` 

### 方法二，优化 if else

```javascript
var fizzBuzz = function (n) {
  if (n == 0) return []
  const result = []
  for (let i = 1; i <= n; i++) {
    result.push(i % 3 == 0 && i % 5 == 0) ? 'FizzBuzz' : i % 3 == 0 ? 'Fizz' : i % 5 == 0 ? 'Buzz' : `${i}`)
  }
  return result
}
```