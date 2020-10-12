## LeetCode 83 删除排序链表中的重复元素

给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

    示例 1:
      输入: 1->1->2
      输出: 1->2

    示例 2:
      输入: 1->1->2->3->3
      输出: 1->2->3

#### 方法一： 遍历链表，赋值不重复的节点
缺点： 增加了 空间复杂度

```javascript
var deleteDuplicates = function (head) {
  if (head == null || head.next == null) return head

  let vHead = new ListNode(), list = new ListNode(head.val)
  while (head) {
    if (head.val !== list.val) {
      list.next = new ListNode(head.val)
      list = list.next
    }
    head = head.next
  }
  return vHead.next
}
```

#### 方法二： 不消耗额外的 空间复杂度

```javascript
var deleteDuplicates = function (head) {
  if (head == null || head.next == null) return head

  const vHead = head
  while (head.next) {
    if (head.val === head.next.val) {
      head.next = head.next.next
    } else {
      head = head.next
    }
  }
  return vHead
}
```