<h2 id="1">LeetCode 200 岛屿数量（连通图个数）</h2>

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。  

岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。  

此外，你可以假设该网格的四条边均被水包围。  

    输入:  
        [ 
        ['1','1','1','1','0'],
        ['1','1','0','1','0'],
        ['1','1','0','0','0'],
        ['0','0','0','0','0']
        ]
    输出: 1


### DFS - 深度优先搜索
1. 使用两层循环，遍历二维数组的每一项
2. 碰到 1 (岛屿)时，则 调用 DFS 的方法，递归的遍历 当前点的 上下左右的点
3. 同时，将访问过的点，置为 0 (水)

```javascript
var numIslands = function (grid) {
    if (grid === null || grid.length === 0) return 0

    let sum = 0
    const rows = grid.length
    const clos = grid[0].length

    const dfs = (r, l) => {
        if (
            r <0 || l < 0 || 
            r >= rows || l >= clos || 
            grid[r][l] === '0'
        ) return
        grid[r][l] = '0'
        dfs(r - 1, l)
        dfs(r + 1, l)
        dfs(r, l - 1)
        dfs(r, l + 1)
    }

    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < clos; j++) {
            if (grid[i][j] === '1') {
                sum++
                dfs(i, j)
            }
        }
    }
    return sum
}
```

### BFS - 广度优先搜索
> 需要借助于一个 队列

1. 两层循环遍历 二维数组，对于每一个未访问过的（见3）岛屿结点，计数 +1
2. 而且都做一次 BFS 搜索
3. 访问过的结点要被标记为 访问过 

```javascript
var numIslands = function (grid) {
    if (grid === null || grid.length === 0) return 0
    let sum = 0
    const rows = grid.length
    const clos = grid[0].length
    const bfs = (r, c) => {
        const dirs = [[1, 0], [0, 1], [-1, 0], [0, -1]]
        const queue = [[r, c]]
        grid[r][c]
        while (queue.length > 0) {
            const curr = queue.shift()
            for (let dir of dirs) {
            const x = curr[0] + dir[0]
            const y = curr[1] + dir[1]
            if (x < 0 || y < 0 || x >= rows || y >= clos || grid[x][y] === '0') continue
            queue.push([x, y])
            grid[x][y] = '0'
            }
        }
    }
    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < clos; j++) {
            if (grid[i][j] === '1') {
                sum++
                bfs(i, j)
            }
        }
    }
    return sum
}
```

#### DFS - 代码模板
##### 首先，我们来看一下 二叉树 DFS 遍历的模板
```javascript
var dfs = (root) => {
    if (root === null) return

    dfs(root.left)
    dfs(root.right)
}
```

##### 图的DFS 遍历模板
```javascript
var inArea = (grid, r, c) => {
    if (
        r < 0 || r > grid.length || 
        c < 0 || c > grid[0].length || 
        visitedMap[grid[r][c]]
    ) {
        return false
    }
    // 通常来说，图的 dfs 要不同于 树的 dfs，因为图可能形成回路，因此，要对访问过的元素打上标记
    visitedMap[grid[r][c]] = true
    return true
}
var dsf = function (grid, r, c) {
    // 验证当前的点，是否有效，即是否是在 grid 的范围内
    if (!inArea(grid, r, c)) return 

    // 遍历当期那点 上下左右 相邻的点
    dfs(grid, r - 1, c)
    dfs(grid, r + 1, c)
    dfs(grid, r, c - 1)
    dfs(grid, r, c + 1)
}
```

**[岛屿类问题的通用解法、DFS 遍历框架](https://leetcode-cn.com/problems/number-of-islands/solution/dao-yu-lei-wen-ti-de-tong-yong-jie-fa-dfs-bian-li-/)**

### 查并集