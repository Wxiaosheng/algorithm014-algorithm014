将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。


    示例：

    输入：1->2->4, 1->3->4
    输出：1->1->2->3->4->4


### 方法一，直接循环，遍历到每一个节点
```javascript
var mergeTwoList = function (l1, l2) {
  if (l1 === null) return l2
  if (l2 === null) return l1
  
  const vHead = new ListNode()
  let temp = vHead
  while (l1 !== null && l2 !== null) {
    if (l1.val <= l2.val) {
      temp.next = new ListNode(l1.val)
      l1 = l1.next
    } else {
      temp.next = new ListNode(l2.val)
      l2 = l2.next
    }
    temp = temp.next
  }
  temp.next = l1 ? l1 : l2
  return vHead.next 
}
```

### 方法二，递归，比较难思考，不易于理解
**在这里说一个误区，本来函数的参数有两个，所以我的第一印象是一个递归(重复子问题)解决两个节点，但是这里并不能一次确定两个节点的位置，一直只能确定一个节点位置，因为当前两个节点中较大的那个节点，不一定是和较小的节点直接链接的**


```JavaScript
var mergeTwoList = function (l1, l2) {
  // 递归函数，一次只能确定一个节点的位置，要特别注意这点，不是一次确定连个节点的位置

  if (l1 === null) return l2
  if (l2 === null) return l1

  if (l1.val <= l2.val) {
    l1.next = mergeTwoList(l1.next, l2)
    return l1
  } else {
    l2.next = mergeTwoList(l1, l2.next)
    return l2
  }
}

```