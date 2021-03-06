<h2 id='1'>LeetCode 102 二叉树的层序遍历</h2>
给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）

    示例：
    二叉树：[3,9,20,null,null,15,7],

        3
       / \
      9  20
        /  \
      15   7
    返回其层次遍历结果：  
    
      [
        [3],
        [9,20],
        [15,7]
      ]

#### 方法一、BFS

```javascript
var levelOrder = function (root) {
  // BFS
  if (root == null) return []

  const result = []
  const queue = [root]
  while (queue.length > 0) {
    const n = queue.length
    const sub = []
    for (let i = 0; i < n; i++) {
      const node = queue.shift()
      sub.push(node.val)
      if (node.left) queue.push(node.left)
      if (node.right) queue.push(node.right)
    }
    result.push(sub)
  }
  return result
};
```

<h2 id='2'>在每个树行中找最大值</h2>
您需要在二叉树的每一行中找到最大的值。示例：

    输入: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

    输出: [1, 3, 9]

#### 方法一、BFS

```javascript
var largestValues = function (root) {
  if (root == null) return []

  const result = []
  const queue = [root]
  while (queue.length) {
    const n = queue.length
    let max
    for (let i = 0; i < n; i++) {
      const node = queue.shift()
      max = max === undefined ? node.val : Math.max(max, node.val)
      if (node.left) queue.push(node.left)
      if (node.right) queue.push(node.right)
    }
    result.push(max)
  }
  return result
}
```