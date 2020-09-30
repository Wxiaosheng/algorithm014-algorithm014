<h2 id="1">LeetCode 36 有效的数独</h2>
判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。

1. 数字 1-9 在每一行只能出现一次。
2. 数字 1-9 在每一列只能出现一次。
3. 数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。

数独部分空格内已填入了数字，空白格用 '.' 表示。

    示例:
      输入:
        [
          ["5","3",".",".","7",".",".",".","."],
          ["6",".",".","1","9","5",".",".","."],
          [".","9","8",".",".",".",".","6","."],
          ["8",".",".",".","6",".",".",".","3"],
          ["4",".",".","8",".","3",".",".","1"],
          ["7",".",".",".","2",".",".",".","6"],
          [".","6",".",".",".",".","2","8","."],
          [".",".",".","4","1","9",".",".","5"],
          [".",".",".",".","8",".",".","7","9"]
        ]
      输出: true

      输入:
        [
          ["8","3",".",".","7",".",".",".","."],
          ["6",".",".","1","9","5",".",".","."],
          [".","9","8",".",".",".",".","6","."],
          ["8",".",".",".","6",".",".",".","3"],
          ["4",".",".","8",".","3",".",".","1"],
          ["7",".",".",".","2",".",".",".","6"],
          [".","6",".",".",".",".","2","8","."],
          [".",".",".","4","1","9",".",".","5"],
          [".",".",".",".","8",".",".","7","9"]
        ]
      输出: false   
      解释: 
        除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。
        但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。

#### 方法一：暴力循环
遍历 邻接矩阵 中的非 `"."` 项，对于每一项 都校验 横、纵 以及 所在九宫格内是否有重复的数字

##### 如何取当前数字所在的 3 X 3 九宫格？
当前数字的坐标为 (r, c)，则 九宫格的 横坐标为 `Math.floor(r / 3) => Math.floor(r / 3) + 3`，纵坐标为 `Math.floor(c / 3) => Math.floor(c / 3) + 3`

```javascript
var isValidSudoku = function (board) {
  var isValid = function (r, c) {
    const rows = [...board.slice(r, 1)]
    rows[c] = '.'
    if (rows.includes(board[r][c])) return false
    const cols = board.map(b => b[c])
    cols[r] = '.'
    if (cols.includes(board[r][c])) return false
    const row = Math.floor(r/3), col = Math.floor(c / 3)
    const subBoard = board.slice(row, row + 3).map(b => b.slice(col, col + 3))
    subBoard[r % 3][c%3] = '.'
    subBoard = subBoard.flat(2)
    if (subBoard.includes(board[r][c])) return false
    return true
  }
  for (let i = 0; i < 9;i++) {
    for (let j = 0; j < 9; j++) {
      if (board[i][j] == '.' && isValid(i, j)) return false
    }
  }
  return true
}
```

#### 方法二：空间换时间
使用 三个变量分别记录，行、列 和 九宫格 中出现的元素

```javascript
var isValidSudoku = function (board) {
  const rows = (new Array(9)).fill(0).map(i => [])
  const cols = (new Array(9)).fill(0).map(i => [])
  const sub = (new Array(9)).fill(0).map(i => [])

  for (let i = 0; i < 9; i++) {
    for (let j = 0; j < 9; j++) {
      const curr = board[i][j]
      if (curr == '.') continue
      if (rows[i].includes(curr)) return false
      else rows[i].push(curr)

      if (cols[j].includes(curr)) return false
      else cols[j].push(curr)

      const r = Math.floor(i / 3) * 3 + Math.floor(j / 3)
      if (sub[r].includes(curr)) return false
      else sub[r].push(curr)
    }
  }
  return true
}
```