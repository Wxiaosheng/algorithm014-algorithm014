<h2 id="1">LeetCode 236 二叉树的最近公共祖先</h2>

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。  

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）”  

    示例 1:

    输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
    输出: 3
    解释: 节点 5 和节点 1 的最近公共祖先是节点 3。

    示例 2:
    输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
    输出: 5
    解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。
     
    说明:
    所有节点的值都是唯一的。
    p、q 为不同节点且均存在于给定的二叉树中。
  

#### 方法一、记录父节点
1、遍历整个二叉树，一次记录每个节点的 父节点
2、从 p 节点开始，向上寻找父节点 并标记为访问过的状态
3、从 q 节点开始，向上寻找父节点，访问到第一个被标记过的节点即为 公共父节点

**注意，这里使用 hashMap 来记录当前节点的父节点，但是不要使用节点对象作为key，这样或导致散列函数的计算时间增加，导致超时**

```javascript
const lowestCommonAncestor = function (root, p, q) {
 const hashMap = {}
  const hashSet = new Set()
  const dfs = function (root) {
    if (root.left !== null) {
      hashMap[root.left.val] = root
      dfs(root.left)
    }
    if (root.right !== null) {
      hashMap[root.right.val] = root
      dfs(root.right)
    }
  }
  dfs(root)
  while (p) {
    hashSet.add(p)
    p = hashMap[p.val]
  }
  while (q) {
    if (hashSet.has(q)) return q
    q = hashMap[q.val]
  }
  return null
}
```

#### 方法二
由**公共祖先的定义**可得到下述结果：
1. p == root，则 q 一定在 root 的左子树或右子树中；
2. q == root，则 p 一定在 root 的左子树或右子树中；
3. p !== root && q == root，则 p、q 一定在 root 的左子树或右子树中；

递归解析：
* 终止条件：
  * 当越过叶节点，则直接返回 null 
  * 当 root 等于 p, qp,q ，则直接返回 root 

* 递推工作：
  * 开启递归左子节点，返回值记为 left 
  * 开启递归右子节点，返回值记为 right 
  
* 返回值： 根据 left 和 right，可展开为四种情况
  1. 当 left 和 right 同时为空：说明 root 的左 / 右子树中都不包含 p,q，返回 null
  2. 当 left 和 right 同时不为空：说明 p, q 分列在 root 的 异侧 （分别在 左 / 右子树），因此 root 为最近公共祖先，返回 root
  3. 当 left 为空 ，right 不为空：p,q 都不在 root 的左子树中，直接返回 right 。具体可分为两种情况：
      * p,q 其中一个在 root 的 右子树 中，此时 right 指向 p（假设为 p ）
      * p,q 两节点都在 root 的 右子树 中，此时的 right 指向 最近公共祖先节点 
  4. 当 left 不为空，right 为空,与情况 3. 同理

```javascript
var lowestCommonAncestor = function (root, p, q) {
  if (root == null || p == root || q == null) return root
  const left = lowestCommonAncestor(root.left, p, q)
  const right = lowestCommonAncestor(root.right, p, q)
  if (left == null && right == null) return null
  if (left == null) return right
  if (right == null) return left
  return root
}
```

<h2 id="2">LeetCode 105 从前序与中序遍历序列构造二叉树</h2>

根据一棵树的前序遍历与中序遍历构造二叉树。

注意: 你可以假设树中没有重复的元素。

例如，给出

    前序遍历 preorder = [3,9,20,15,7]
    中序遍历 inorder = [9,3,15,20,7]
    返回如下的二叉树：

       3
      / \
     9  20
       /  \
      15   7


#### 方法一
Tree 的遍历一般是通过递归得到的，那么其实构建一课树，也可以通过递归得到，关键是拆分出 **最小重复子问题**

1. 根据前序遍历的结果可以得到，第一个元素即为当前树的根结点的值，创建当前根结点
2. 在中序遍历的结果中找到根结点的位置，此时可以确定当前树的左右子树的个数以及对应的中序遍历的结果
3. 根据左右子树的个数，拆分前序遍历的结果，分别得到左右子树的前序遍历结果
4. 递归，创建当前根结点的左右子树

```javascript
var buildTree = function (preorder, inorder) {
  // terminator
  if (preorder.length == 0) return null
  if (preorder.length == 1) return new TreeNode(preorder[0])
  // process current logic
  // 创建当前树的 根结点
  const root = new TreeNode(preorder[0])
  // 得到根结点在 inorder 中的位置
  const rootInorderIndex = inorder.indexOf(preorder[0])
  // 递归创建 左右子树
  root.left = buildTree(preorder.slice(1, rootInorderIndex + 1), inorder.slice(0, rootInorderIndex))
  root.right = buildTree(preorder.slice(rootInorderIndex + 1), inorder.slice(rootInorderIndex + 1))
  return root
}
```

#### 方法二、我暂时理解不了递归的解法