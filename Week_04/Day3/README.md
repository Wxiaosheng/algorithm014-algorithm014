<h2 id='1'>LeetCode 127 单词接龙</h2>

给定两个单词（beginWord 和 endWord）和一个字典，找到从 beginWord 到 endWord 的最短转换序列的长度。转换需遵循如下规则：

1. 每次转换只能改变一个字母。
2. 转换过程中的中间单词必须是字典中的单词。

说明:
* 如果不存在这样的转换序列，返回 0。
* 所有单词具有相同的长度。
* 所有单词只由小写字母组成。
* 字典中不存在重复的单词。
* 你可以假设 beginWord 和 endWord 是非空的，且二者不相同。

#### 构建无向图 + BFS
通过 beginWord 为根节点，枚举单词的每一位，同时替换成 a-z，对于存在 wordList 的字符串，构建成向外扩散成一个 无向图  

当其中的一个结点与 endWord 相等时，则找到最小路径 (BFS)

```javascript
var ladderLength = function (beginWord, endWord, wordList) {
  if (!wordList.includes(endWord)) return 0

  const wn = beginWord.length
  const hash = new Set(wordList) // 方便判断生成的字符串是否在字典中
  const visited = new Set() // 记录已访问的结点
  const queue = [beginWord]
  visited.add(beginWord)

  let step = 1

  while (queue.length) {
    const n = queue.length
    // BFS 遍历 Graph 每一层
    for (let i = 0; i < n; i++) {
      const str_arr = queue.shift().split('')
      for (let j = 0; j < wn; j++) {
        const originChar = str_arr[j]
        for (let k = 0; k < 26; k++) {
          const char = String.fromCharCode(97 + k)
          if (char == originChar) continue
            str_arr[j] = char
          const nextStr = str_arr.join('')
          // 非字典中元素，不处理
          if (hash.has(nextStr)) {
            // 找到 endWord
            if (nextStr == endWord) return step+1
            // 未访问过的结点 才加入 queue
            if (!visited.has(nextStr)) {
              queue.push(nextStr)
              visited.add(nextStr)
            }
          }
        }
        str_arr[j] = originChar
      }
    }
    step++
  }
  return 0
}
```

#### 优化后的 BFS
```javascript
var ladderLength = function (beginWord, endWord, wordList) {
  if (wordList.length == 0 || !wordList.includes(endWord)) return 0

  const hash = new Set(wordList)
  const visited = new Set()
  const queue = [[beginWord, 1]]
  visited.add(beginWord)

  while (queue.length) {
    const [str, count] = queue.shift()
    if (str == endWord) return count
    for (let i = 0; i < str.length; i++) {
      for (let j = 0; j < 26; j++) {
        const char = String.fromCharCode(97 + j)
        if (char == str[i]) continue
        const nextStr = `${str.slice(0, i)}${char}${str.slice(i + 1)}`
        if (hash.hash(nextStr) && !visited.has(nextStr)) {
          queue.push([nextStr, count + 1])
          visited.add(nextStr)
        }
      }
    }
  }
  return 0
}
```

#### 双向 BFS
> 前提必须是 起点 和 终点 必须是已知的

