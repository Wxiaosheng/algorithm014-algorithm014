<h2 id="1">LeetCode 617 合并二叉树</h2>

给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点。

示例 1:

    输入: 
      Tree 1                     Tree 2                  
             1                        2                             
            / \                       / \                            
           3   2                    1   3                        
          /                           \   \                      
         5                             4   7                  
    输出: 
    合并后的树:
           3
          / \
         4   5
        / \   \ 
       5   4   7

注意: 合并必须从两个树的根节点开始。


#### 方法一： recursion
`recursion` 递归的最关键点为，寻找 **最小重复子问题**  

本题中，最小重复子问题为： 同一棵树的相同位置的节点，都要做相同的处理

```javascript
var mergeTrees = function (t1, t2) {
  if (t1 == null && t2 == null) return null
  if (t1 == null) return t2
  if (t2 == null) return t1

  const node = new TreeNode(t1.val + t2.val)
  node.left = mergeTrees(t1.left, t2.left)
  node.right = mergeTrees(t1.right, t2.right)
  return node
}
```

<h2 id="2">LeetCode 130 被围绕的区域</h2>
给定一个二维的矩阵，包含 'X' 和 'O'（字母 O）。

找到所有被 'X' 围绕的区域，并将这些区域里所有的 'O' 用 'X' 填充。

    示例:
      X X X X
      X O O X
      X X O X
      X O X X

    运行你的函数后，矩阵变为：
      X X X X
      X X X X
      X X X X
      X O X X

解释:  
被围绕的区间不会存在于边界上，换句话说，任何边界上的 'O' 都不会被填充为 'X'。 任何不在边界上，或不与边界上的 'O' 相连的 'O' 最终都会被填充为 'X'。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。

#### 方法一：Breadth First Search
原本的思路是，遍历 邻接矩阵，对每一个 'O' 元素都进行 BFS 递归，找出当前元素以及与当前元素链接的 'O' 元素 是否有 上下左右边界，在开发的过程中发现 上下左右的边界难以判断，甚至判断不了

然后看题解，解题的思路为，由于能确定 边界上的 'O' 元素一定不会被包围，因此 BFS 找到边界'O'元素所有直接相连的 'O' 并且标记，最后 遍历邻接矩阵 内部的所有元素（可以排除边界），将 未被标记的 'O' 改成 'X'

```javascript
var solve = function (board) {
  if (board.length == 0 || board[0].length == 0) return board
  const m = board.length, n = board[0].length, hash = new Set(), visited = new Set()

  // 广度优先搜索 （标记）hash记录 与边界相连的 O
  const bfs = function (r, c) {
    if (
      r < 0 || r >= m ||
      c < 0 || c >= n ||
      board[r][c] == 'X' ||
      visited.has([r, c].join(','))
    ) return 
    hash.add(r, c].join(','))
    visited.add(r, c].join(','))

    bfs(r + 1, c)
    bfs(r - 1, c)
    bfs(r, c + 1)
    bfs(r, c - 1)
  }

  // 遍历边界上的 'O'
  for (let i = 0; i < m; i++) {
    if (board[i][0] == 'O') bfs(i, 0)
    if (board[i][n-1] == 'O') bfs(i, n-1)
  }
  for (let j = 0; j < n; j++) {
    if (board[0][j] == 'O') bfs(0, j)
    if (board[m-1][j] == 'O') bfs(m-1, j)
  }
  
  for (let i = 1; i < m - 1; i++) {
    for (let j = 1; j < n - 1; j++) {
      if (board[i][j] == 'O' && !hash.has([i, j].join(','))) board[i][j] = 'X'
    }
  }
  return board
}
```