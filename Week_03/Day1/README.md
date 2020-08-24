<h2 id="1">LeetCode 22 括号生成</h2>
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

    示例：

    输入：n = 3
    输出：[
        "((()))",
        "(()())",
        "(())()",
        "()(())",
        "()()()"
        ]

### 方法一、自己想出来的解法
    数学归纳法：

    1  =>  '()'
    2  =>  '()()'、'(())'
    3  =>  '()()()'、'(())()'、'()(())'、'(()())'、'((()))'

    n = 2时，可以看成将一对括号 `()` 插入到 n = 1时的字符串上，可插入的位置是字符串 `()` 的前面，中间，和后面三个地方，恰好正是该字符串的可遍历的 index 索引值

    n = 3时，同理，可以看成将一对括号 `()` 插入到 n = 2时每个字符串可插入的位置，注意会有重复的值出现，所以我们需要去重

```javascript
var generateParenthesis = function (n) {
    // terminator
    if (n == 0) return []
    if (n == 1) return ['()']
    const s = new Set()
    // drill down
    const result = generateParenthesis(n - 1)
    // proess current logic
    for (let item of result) {
        for (let i = 0; i < item.length; i++) {
            s.add(`${item.slice(0, i)}()${item.slice(i, item.length)}`)
        }
    }
    return Array.form(s)
    // restore current status
}
```

使用上课的递归四步走的写法如下

```JavaScript
var generateParenthesis = function (n) {
    if (n == 0) return []
    const helper = function (level, result) {
        // terminator
        if (level >= n) {
            return result
        }
        // proess current logic
        const s = new Set()
        for (let item of result) {
            for (let i = 0; i < item.length; i++) {
                s.add(`${item.slice(0, i)}()${item.slice(i, item.length)}`)
            }
        }
        // drill down
        return helper(level + 1, Array.form(s))
        // restore
    }
    return helper(1, ['()'])
}
```


### 方法二、课上解题方法
将字符串看成一个由 `'('` 和 `')'` 组成的2 * n 位的字符串，枚举所有的情况，然后验证合法性

```javascript
var generateParenthesis = function (n) {
    const result = []
    const helper = function (level, max, str) {
        // terminator
        if (level >= max) {
            // 需要验证 str 的合法性，才能作为最后的结果 push
            return result.push(str)
        }
        // proess current logic
        // drill down
        helper(level + 1, max, str + '(')
        helper(level + 1, max, str + ')')
    }
    helper(0, 2 * n, '')
    return result
}
```

**优化：**
1. 在添加的时候就保证合法性
2. `'('` 只要没有超过 n，就可以随意添加
3. `')'` 只要没有超过 `'('` 的个数即可

```javascript 
var generateParenthesis = function (n) {
    const result = []
    const helper = function (left, right, n, str) {
        // terminator
        if (left >= n && right >= n) {
            return result.push(str)
        }
        // proess current logic
        // drill down
        if (left < n) { 
            helper(left + 1, right, n, str + '(')
        }
        if (left > right) {
            helper(left, right + 1, n, str + ')')
        }
    }
    helper(0, 0, n, '')
    return result
}
```