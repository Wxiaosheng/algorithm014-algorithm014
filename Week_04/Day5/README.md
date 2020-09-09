<h2 id='1'>LeetCode 874 模拟行走机器人</h2>
机器人在一个无限大小的网格上行走，从点 (0, 0) 处开始出发，面向北方。该机器人可以接收以

下三种类型的命令：
* -2：向左转 90 度  
* -1：向右转 90 度
* 1 <= x <= 9：向前移动 x 个单位长度

在网格上有一些格子被视为障碍物, 第 i 个障碍物位于网格点  (obstacles[i][0], obstacles[i][1])

机器人无法走到障碍物上，它将会停留在障碍物的前一个网格方块上，但仍然可以继续该路线的其余部分。

返回从原点到机器人所有经过的路径点（坐标为整数）的最大欧式距离的平方。

#### 方法一，分析法
1. 机器人只有两种行为，转向 和 行走
2. 定义变量记住方向
3. 定义 Set 记录障碍物，走向下一步之前，先判断下一步是否是障碍物
4. 行走，记录并更新 横纵坐标
5. 记录最大 欧氏距离

```javascript
var robotSim = function (commands, obstacles) {
  if (commands.length == 0) return 0

  let x = 0, y = 0, dx = 0, dy = 1, max = 0
  // 存储障碍物
  const hash = new Set()
  obstacles.forEach(o => hash.add(`${o[0]},${o[1]}`))

  for (let i = 0; i < commands.length; i++) {
    const curr = commands[i]
    if (curr == -1) { // 右转
      if (dx == 1) {
          dx = 0, dy = -1
      } else if (dx == -1) {
          dx = 0, dy = 1
      } else if (dy == 1) {
          dx = 1, dy = 0
      } else {
          dx = -1, dy = 0
      }
    } else if (curr == -2) { // 左转
      if (dx == 1) {
          dx = 0, dy = 1
      } else if (dx == -1) {
          dx = 0, dy = -1
      } else if (dy == 1) {
          dx = -1, dy = 0
      } else {
          dx = 1, dy = 0
      }
    } else { // 行走
      for (let j = 1; j <= curr; j++) {
        let nx = x + dx * 1, ny = y + dy * 1
        if (!hash.has(`${nx},${ny}`)) {
          x = nx, y = ny
        }
      }
      max = Math.max(max, Math.pow(x, 2) + Math.pow(y, 2))
    }
  }
  return max
}
```

#### 方法二，优化方向的判断 和 更新

```javascript
var robotSim = function (commands, obstacles) {
  if (commands.length == 0) return 0

  let x = 0, y = 0, d = 0, max = 0
  const hash = new Set()
  const dirts = [[0,1],[1,0],[0,-1],[-1,0]]
  obstacles.forEach(o => hash.add(`${o[0]},${o[1]}`))
  for (let c of commands) {
    if (c < 0) {
      d = c == -1 ? (d+1) %4 : (d+3)%4
    } else {
      for (let i = 1; i <= c; i++) {
        let nx = x + dirts[d][0], ny = y + dirts[d][1] 
        if (!hash.has(`${nx},${ny}`)) x = nx, y = ny
        max = Math.max(max, Math.pow(x, 2) + Math.pow(y, 2))
      }
    }
  } 
  return max
} 
```

##### 2020年9月9日 每日一题
```javascript
var robotSum = function (commands, obstacles) {
  if (commands.length == 0) return 0
  let x = 0, y = 0, d = 0, result = 0
  const directs = [[0,1], [1,0], [0, -1], [-1,0]]
  const obsSet = new Set(obstacles.map(o => o.join(',')))
  const handleCommand = function (n) {
    if (n = -2) d = (d + 3) % 4
    if (n = -1) d = (d + 1) % 4
    for (let i = 1; i <= n; i++) {
      const nx = x + directs[d][0], ny = y + directs[d][1]
      if (!obsSet.has([nx, ny].join(','))) x = nx, y = ny
    }
    result = Math.max(result, Math.pow(x, 2) + Math.pow(y, 2))
  }
  for (let i = 0; i < commands.length; i++) {
    handleCommand(commands[i])
  }
  return result
}
```

<h2 id='2'>LeetCode 55 跳跃游戏</h2>

#### 方法一，遍历每一个位置，记录当前能到达的路径

```javascript
var canJump = function (nums) {
  if (nums.length < 2) return true
  const result = (new Array(nums.length)).fill(false)
  result[0] = true
  for (let i = 0; i < nums.length - 1; i++) {
    // 减枝
    if (!result[i]) return false
    if (i + nums[i] >= nums.length - 1) return true
    while (nums[i] > 0) result[i + nums[i]--] = true
  }
  return result.filter(r => !r).length == 0
}
```

### 方法二，贪心算法，循环每一个元素，确定能走的最大距离

```javascript
var canJump = function (nums) {
  if (nums.length < 2) return true
  if (nums.length < 2) return true
  let max = 0
  for (let i = 0; i < nums.length; i++) {
    if (i <= max) max = Math.max(max, i + nums[i])
  }
  return max >= nums.length - 1
}
```

##### 上面方法还可以进一步减支
```javascript
var canJump = function (nums) {
  if (nums.length < 2) return true
  if (nums.length < 2) return true
  let max = 0
  for (let i = 0; i < nums.length; i++) {
    if (i <= max) max = Math.max(max, i + nums[i])
    // 减支
    if (max >= nums.length - 1) return true
  }
  return max >= nums.length - 1
}
```