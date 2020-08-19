<h2 id="1">N 叉树的前序遍历</h2>

给定一个 N 叉树，返回其节点值的前序遍历。

### 方法一，简便写法 递归 + ...

```javascript
var preorder = function (node) {
  if (root === null) return []

  return [
    node.val,
    ...(node.children.map(c => preorder(c)).flat(2))
  ]
}
```

### 方法二，递归 + 辅助函数

```javascript
var preorder = function (root) {
  const result = []
  const helper = function (node) {
    if (node === null) return []
    result.push(node.val)
    node.children.forEach(c => helper(c))
  }
  helper(root)
  return result
}
```

### 迭代法，不太好理解，模板都是相同的，要注意的是，前序 和 后序 遍历时，子节点的入栈顺序不同，而且当前节点加入结果中的位置也不同

```javascript
var preorder = function (root) {
  if (root === null) return []
  const result = []
  const stack = [root]
  while (stack.length > 0) {
    const node = stack.pop()
    result.push(node.val)
    for (let i = node.children.length - 1; i >= 0; i--) {
      stack.push(node.children[i])
    }
  }
  return result
}
```


<h2 id="2">N 叉树的后序遍历</h2>

给定一个 N 叉树，返回其节点值的后序遍历。

### 方法一，迭代 + ...

```javascript
var postorder = function (root) {
  if (root === null) return []
  return [
    ...(root.children.map(c => postorder(c)).flat(2)),
    node.val
  ]
}
```

### 方法二， 迭代 + 辅助函数

```javascript
var postorder = function (root) {
  const result = []
  const helper = node => {
    if (node === null) return []
    node.children.forEach(c => helper(c))
    result.push(node.val)
  }
  helper(root)
  return result
}
```

### 方法三， 迭代，模板都是一个套路，但是要注意的是，前序 和 后序遍历时，访问子节点的顺序不同，而且当前节点加入节点中的位置也不同

```javascript
var postorder = function (root) {
  if (root === null) return []
  const result = []
  const stack = [root]
  while (stack.length > 0) {
    const node = stack.pop()
    for (let c of node.children) {
      stack.push(c)
    }
    result.push(node.val)
  }
  return result.reverse()
}
// 或者 还是使用 result.unshift(node.val)，但是返回值不需要反转， return result
```
