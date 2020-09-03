<>

<h2 id='2'>LeetCode 433 最小基因变化</h2>
一条基因序列由一个带有8个字符的字符串表示，其中每个字符都属于 "A", "C", "G", "T"中的任意一个。

假设我们要调查一个基因序列的变化。一次基因变化意味着这个基因序列中的一个字符发生了变化。

例如，基因序列由"AACCGGTT" 变化至 "AACCGGTA" 即发生了一次基因变化。

与此同时，每一次基因变化的结果，都需要是一个合法的基因串，即该结果属于一个基因库。

现在给定3个参数 — start, end, bank，分别代表起始基因序列，目标基因序列及基因库，请找出能够使起始基因序列变化为目标基因序列所需的最少变化次数。如果无法实现目标变化，请返回 -1。

注意:
1. 起始基因序列默认是合法的，但是它并不一定会出现在基因库中。
2. 所有的目标基因序列必须是合法的。
3. 假定起始基因序列与目标基因序列是不一样的。


#### 方法一：构建无向图 + BFS
> 只能用于找次数， 不能用于找路径

```javascript
var minMutation = function (start, end, bank) {
  if (bank.length == 0 || !bank.includes(end)) return -1

  const hash = new Set(bank)
  const visited = new Set()
  const queue = [start]
  visited.add(start)

  let step = 0
  while (queue.length) {
    step++
    const n = queue.length
    // 遍历 无向图 的每一层
    for (let i = 0; i < n; i++) {
      const str = queue.shift()
      // 枚举所有可能的变化
      for (let j = 0; j < 8; j++) {
        for (let c of ["A", "C", "G", "T"]) {
          const nextStr = `${str.slice(0, j)}${c}${str.slice(j + 1)}`
          if (str == nextStr) continue
          if (hash.has(nextStr)) {
            if (nextStr == end) return step
            if (!visited.has(nextStr)) {
              queue.push(nextStr)
              visited.add(nextStr)
            }
          }
        }
      }
    }
  }
  return -1
}
```

#### 优化后的 BFS
> 少了一层 BFS 固定的 for 循环，因为这里不需要处理分层，所以可以被优化掉

```javascript
var minMutation = function () {
    if (bank.length == 0 || !bank.includes(end)) return -1

  const base = ["A", "C", "G", "T"]
  const hash = new Set(bank)
  const visited = new Set()
  const queue = [[start, 0]]
  visited.add(start)

  while (queue.length) {
    const [str, count] = queue.shift()
    for (let i = 0; i < str.lengt; i++) {
      for (let c of base) {
        const nextStr = `${str.sicle(i, j)}${c}${str.slice(j + 1)}`
        if (nextStr == str) continue
        if (hash.has(nextStr) && !visited.has(nextStr)) {
          queue.push([nextStr, count + 1])
          visited.add(nextStr)
        }
      }
    } 
  }
  return -1
}
```