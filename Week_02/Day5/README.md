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


### DFS 
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