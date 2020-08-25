<h2 id="1">LeetCode 226 翻转二叉树</h2>
翻转一棵二叉树。

    示例：
      输入：

          4
        /   \
        2     7
      / \    / \
    1   3  6   9
      
      输出：

          4
        /   \
        7     2
      / \   / \
      9   6 3   1

#### 解法一、递归
使用递归模板，解答该题

```javascript
var invertTree = function (root) {
  const helper = function (level, root) {
    // terimator
    if (root == null) return root
    // process current logic
    // drill down
    const temp = root.left
    root.left = helper(root.right)
    root.right = helper(temp)
    return root
    // restore
  }
  return helper(1, root)
}
```

最后我们大概率会得到上述这样的代码，其实这段带可以被优化成更优雅的形式

```javascript
// 一共 5 行 代码
var invertTree = function (root) {
  if (root == null) return root
  const temp = root.left
  root.left = helper(root.right)
  root.right = helper(temp)
  return root
}
```

#### 迭代
通常能用递归实现的，一般情况下也能使用 循环实现，主要要使用额外的数据结构 Stack 或 Queue 来 模拟 **函数调用栈**

```javascript
var invertTree = function(root) {
  if (root == null) return root
  const queue = [root]
  while (queue.length > 0) {
    const node = queue.shift()
    const temp = node.left
    node.left = node.right
    node.right = temp
    if (node.left) queue.push(node.left)
    if (node.right) queue.push(node.right)
  }
  return root
};
```