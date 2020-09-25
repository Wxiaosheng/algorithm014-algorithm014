<h2 id="1">LeetCode 106 从中序与后序遍历序列构造二叉树</h2>
根据一棵树的中序遍历与后序遍历构造二叉树。

注意: 你可以假设树中没有重复的元素。

    例如，给出
      中序遍历 inorder = [9,3,15,20,7]
      后序遍历 postorder = [9,15,7,20,3]

    返回如下的二叉树：
         3
        / \
       9  20
         /  \
        15   7

#### 方法一： recursion
**寻找 最小重复子问题**

```javascript
var buildTree = function(inorder, postorder) {
  if (inorder.length == 0) return null
  const n = postorder.length, rootVal = postorder[n - 1]
  const rootIdx = inorder.indexOf(rootVal)
  const root = new TreeNode(rootVal)
  root.left = buildTree(inorder.slice(0, rootIdx), postorder.slice(0, rootIdx))
  root.right = buildTree(inorder.slice(rootIdx + 1), postorder.slice(rootIdx, n - 1))
  return root
}
```