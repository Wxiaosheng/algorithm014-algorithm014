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


### LeetCode 20 有效的括号
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
