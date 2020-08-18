<h2 id="1">LeetCode 94 二叉树的中序遍历</h2>

### 方法一，由于需要一个变量保存所有的结果，因此需要单独再开一个函数，来共享数据的存储

```javascript
var inorderTraversal  = function (root) {
  const result = []
  const helper = (node) => {
    if (node === null) return []
    helper(node.left)
    result.push(node.val)
    helper(node.right)
  }
  helper(root)
  return result
}
```

### 方法二，使用栈，中序遍历需要保存访问路径

```javascript
var inorderTraversal = function (root) {
  const result = []
  const stack = []
  while (root !== null || stack.length > 0) {
    if (root !== null) {
      stack.push(root)
      root = root.left
    } else {
      const node = stack.pop()
      result.push(node.val)
      root = node.right
    }
  }
  return result
}
```

### 方法三，个人的解法

```javascript
var inorderTraversal = function (root) {
  if (root === null) return []
  return [
    ...inorderTraversal(root.left), 
    root.val, 
    ...inorderTraversal(root.right)
  ]
}
```

<h2 id="2">LeetCode 144 二叉树的前序遍历</h2>

> 与中序相似

<h2 id="3">LeetCode 94 二叉树的后序遍历</h2>

> 与中序相似