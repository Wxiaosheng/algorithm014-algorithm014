## LeetCode 100 相同的树

给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

### 思路，检查两颗树对应的每一个节点，如果有不同的则不相等，直到遍历完所有节点都没找到不同的节点，两棵树是相同的树

**Depth First Search**

```javascript 
var isSameTree = function (p, q) {
  const compareTree = (t1, t2) => {
    if (t1 === null && t2 !== null) return false
    if (t1 !== null && t2 === null) return false
    if (t1 === null && t2 === null) return true
    return t1.val === t2.val && helper(t1.left, t2.left) && helper(t1.right, t2.right)
  }
  return compareTree(p, q)
}
```