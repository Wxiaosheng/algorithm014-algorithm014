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

<h2 id="2">LeetCode 98 验证二叉搜索树</h2>
给定一个二叉树，判断其是否是一个有效的二叉搜索树。  

假设一个二叉搜索树具有如下特征：  
  * 节点的左子树只包含小于当前节点的数。
  * 节点的右子树只包含大于当前节点的数。
  * 所有左子树和右子树自身必须也是二叉搜索树。

示例

    输入:
        2
        / \
      1   3
    输出: true

    输入:
        5
        / \
      1   4
         / \
        3   6
    输出: false

    解释: 输入为: [5,1,4,null,null,3,6]
         根节点的值为 5 ，但是其右子节点值为 4 
  
#### 方法一、中序遍历二叉树，二叉搜索树的中序遍历结果是升序的

```javascript
var isValidBST = function (root) {
  if (root == null) return []
  const result = [...isValidBST(root.left), root.val, ...isValidBST(root.right)]
  for (let i = 1; i < result.length; i++) {
    if (result[i] <= result[i - 1]) return false
  }
  return true
}
```
对于这种方法，能进一步优化，在每次获取当前节点的值时，判断与前一个节点的大小

```javascript
var isValidBST = function (root) {
  const result = []
  const helper = function (node) {
    if (node == null) return true
    let left = helper(root.left)
    let curr = true
    if (result.length > 0) curr = result[result.length - 1] < node.val
    result.push(node.val)
    let right = helper(root.right)
    return left && curr && right
  }
  return helper(root)
}
```

但是这种方法增加了空间复杂度，还可以优化空间复杂度

```javascript
var isVaildBST = function (root) {
  if (root == null) return true
  let prev
  const helper = function (node) {
    if (node == null) return true
    const left = helper(node.left)
    let curr = true
    if (prev !== undefined) {
      curr = prev < node.val
    }
    prev = node.val
    const right = helper(node.right)
    return left && curr && right
  }
  return helper(root)
}
```

### 递归较优解法
```javascript
var isVildBST = function (root) {
  let prev
  const helper = function (node) {
    if (node == null) return true
    if (!helper(node.left)) return false
    if (prev !== undefined) {
      if (prev >= node.val) return false
    }
    prev = node.val
    return helper(node.right)
  }
  return helper(root)
}
```
