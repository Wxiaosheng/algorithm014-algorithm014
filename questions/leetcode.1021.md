## LeetCode 1021 删除最外层的括号
有效括号字符串为空 ("")、"(" + A + ")" 或 A + B，其中 A 和 B 都是有效的括号字符串，+ 代表字符串的连接。例如，""，"()"，"(())()" 和 "(()(()))" 都是有效的括号字符串。  

如果有效字符串 S 非空，且不存在将其拆分为 S = A+B 的方法，我们称其为原语（primitive），其中 A 和 B 都是非空有效括号字符串。  

给出一个非空有效字符串 S，考虑将其进行原语化分解，使得：S = P_1 + P_2 + ... + P_k，其中 P_i 是有效括号字符串原语。  

对 S 进行原语化分解，删除分解中每个原语字符串的最外层括号，返回 S 。  

### 方法一，使用栈
1. 使用栈时，需要特殊处理栈的长度为 1 时的情况
2. loop 时，当前字符为 '('，如果栈的长度大于 0（即，不为最外层），则 拼接该字符，该字符入栈
3. loop 时，当前字符为 ')'，如果栈的长度大于 1（即，不为最外层），则 拼接该字符，出一次栈

```javascript
var removeOuterParentheses = function (S) {
  let res = '', stack = []
  for (let s of S) {
    if (s === '(') {
      if (stack.length > 0) res += s
      stack.push(s)
    } else {
      if (stack.length > 1) res += s
      stack.pop()
    }
  }
  return res
}
```

### 方法二、计数法
1. 记录一个 **原语** 的其实位置和结束位置 
2. 每次遇见一个 **原语** 的结束位置，都拼接一次结果

```javascript
var removeOuterParentheses = function (S) {
  let res = '', count = 0
  for (let i = 0; i < S.length; i++) {
    if (count === 0) start = i
    S[i] === '(' ? count++ : count--
    if (count === 0) {
      res += S.substr(start + 1, i - start + 1 - 2)
    }
  }
  return res
}
```

### 方法三、记录是否是最外层，拼接省略最外层
1. 定一个一个变量，记录是否是最外层
2. 如果是最外层层，则跳过拼接

```javascript
var removeOuterParentheses  = function (S) {
  let res = '', count = 0
  for (s of S) {
    if (s === '(' && count++ > 0) res += s
    if (s === ')' && count-- > 1) res += s
  }
  return res
}
```