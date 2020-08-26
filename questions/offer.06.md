## 剑指offer 06 从尾到头打印链表
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

    示例 1：
    输入：head = [1,3,2]
    输出：[2,3,1]
    限制：0 <= 链表长度 <= 10000


#### 方法一，遍历整个链表，将结果存在一个 数组中，最后返回时，反转该数组

```javascript
var reversePrint = function (head) {
  if (head == null) return []
  const result = []
  while (head !== null) {
    result.push(head.val)
    head = head.next
  }
  return result.reverse()
}
```

#### 方法二、递归

```javascript
var reversePrint = function (head) {
  const helper = function (head, result) {
    if (head == null) return result
    result.unshift(head.val)
    return helper(head.next, result)
  }
  return helper(head, [])
}
```

递归的方式，可以更加优雅

```javascript
var reversePrint = function (head) {
  if (head == null) return []
  return [...reversePrint(head.next), head.val]
}
```
