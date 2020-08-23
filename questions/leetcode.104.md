## LeetCode 104 二叉树的最大深度
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

    示例：
    给定二叉树 [3,9,20,null,null,15,7]，

       3
      / \
      9  20
        /  \
      15   7
    返回它的最大深度 3 。

### 方法一， Depth First Search

```javascript
var maxDepth = function (root) {
  if (root == null) return 0

  let level = 0
  const helper = (node, l) => {
    level = Math.max(level, l)
    if (node.left) helper(node.left, l + 1)
    if (node.right) helper(node.right, l + 1)
  }
  helper(root, 1)
  return level
}
```

### 方法二，优化后的 递归

```javascript
var maxDepth = function (root) {
  if (root == null) return 0
  return Math.max(MaxDepth(root.left), maxDepth(root.right)) + 1
}
```

### 方法三、 Breadth First Search

```javascript
var maxDepth = function (root) {
  if (root == null) return 0

  let level = 0
  const queue = [root]
  while (queue.length > 0) {
    const length = queue.length
    for (let i = 0; i < length; i++) {
      const node = queue.shift()
      if (node.left) queue.push(node.left)
      if (node.right) queue.push(node.right)
    }
    level ++
  }
  return level
}
```