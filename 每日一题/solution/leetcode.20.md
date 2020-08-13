## LeetCode 20: 有效的括号
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效

有效字符串需满足：
1. 左括号必须用相同类型的右括号闭合
2. 左括号必须以正确的顺序闭合
3. 注意空字符串可被认为是有效字符串

### 方法一，由于括号的匹配规则，第一个出现的右括号肯定是要于当前最后一个左括号匹配，这样很适合栈的数据结构

```js
var isValid = function(s) {
  if (s === "") return true
  // 奇数位字符串，肯定不合法
  if (s.length % 2 === 1) return false

  const stack = []
  const hash = {
    ')': '(',
    ']': '[',
    '}': '{'
  }
  for (let i = 0; i < s.length; i++) {
    if (s[i] === ')' || s[i] === ']' || s[i] === '}') {
      if (hash[s[i]] !== stack.pop()) {
        return false
      }
    } else {
      stack.push(s[i])
    }
  }
  return stack.length === 0
};
```


### 方法二，比较巧妙，由于给定字符串中，仅包含括号，所以可以将字符串中的括号成对的替换成 ""，看最后的结果是否为 ""

```js
var isValid = function(s) {
  if (s === "") return true
  // 奇数位字符串，肯定不合法
  if (s.length % 2 === 1) return false

  while (s.includes("()") || s.includes("[]") || s.includes("{}")) {
    s = s.replace("()", "")
    s = s.replace("[]", "")
    s = s.replace("{}", "")
  }
  return s === ""
};
```