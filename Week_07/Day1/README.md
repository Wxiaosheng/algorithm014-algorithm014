<h2 id="1">LeetCode 538 把二叉搜索树转换为累加树</h2>

给定一个二叉搜索树（Binary Search Tree），把它转换成为累加树（Greater Tree)，使得每个节点的值是原来的节点值加上所有大于它的节点值之和。

    例如：

    输入: 原始二叉搜索树:
              5
            /   \
            2     13

    输出: 转换为累加树:
              18
            /   \
          20     13

#### 方法一： recursion
利用 BST 的遍历结果是有序的 特点，可以使用 `后序遍历法` 得到的结果是 倒叙的

```javascript
var convertBST = function (root) {
  if (root == null) return root
  let preSum = 0
  const helper = function (node) {
    // terminator
    if (node == null) return
    // process current logic
    helper(node.right)
    root.val = root.val + preSum
    preSum = root.val
    helper(node.left)
    // dirll down
    // restore
  }
  helper(root)
  return root
}
```