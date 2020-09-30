<h2 id="1">LeetCode 107 二叉搜索树中的插入操作</h2>
给定二叉搜索树（BST）的根节点和要插入树中的值，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。 输入数据保证，新值和原始二叉搜索树中的任意节点值都不同。

注意，可能存在多种有效的插入方式，只要树在插入后仍保持为二叉搜索树即可。 你可以返回任意有效的结果。

提示：
* 给定的树上的节点数介于 0 和 10^4 之间
* 每个节点都有一个唯一整数值，取值范围从 0 到 10^8
* -10^8 <= val <= 10^8
* 新值和原始二叉搜索树中的任意节点值都不同

#### 方法一： 递归 - recursion
**找到最小重复子问题， 即 无节点、一个节点、两个节点的 BST 改如何插入节点**

```javascript
var insertIntoBST = function (root, val) {
  if (root == null) return new TreeNode(val)
  if (val < root.val) {
    if (root.left) insertIntoBST(root.left, val)
    else root.left = new TreeNode(val)
  }
  if (val > root.val) {
    if (root.right) insertIntoBST(root.right, val)
    else root.right = new TreeNode(val)
  }
  return root
}
```

#### 方法二： 迭代 - BFS
> 本题不太适合 DFS，而 DFS 更加适合

```javascript
var insertIntoBST = function (root, val) {
  if (root == null) return new TreeNode(val)
  const queue = [root]
  while (queue.length) {
    const node = queue.shift()
    if (val < node.val) {
      if (node.left) queue.push(node.left)
      else {
        root.left = new TreeNode(val)
        break
      }
    } else {
      if (node.right) queue.push(node.right)
      else {
        root.right = new TreeNode(val)
        break
      }
    }
  }
  return root
}
```
