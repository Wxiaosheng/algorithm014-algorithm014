## LeetCode 25 K 个一组翻转链表

给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。  
k 是一个正整数，它的值小于或等于链表的长度。  
如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。  

示例：  
给你这个链表：1->2->3->4->5  
当 k = 2 时，应当返回: 2->1->4->3->5  
当 k = 3 时，应当返回: 3->2->1->4->5  
 
说明：  
你的算法只能使用常数的额外空间。  
你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。  

#### 方法
**将链表以每份 k 个分成 n 份，同时记录每一份的前一节点和后一节，用于反转链表**

```javascript
var reverseList= (head, end) => {
  let prev = end.next
  let p = head
  while (prev !== end) {
    const next = p.next
    p.next = prev
    prev = p
    p = next
  }
  return [end, head]
}
var reverseKGroup = function (head, k) {
  if (head === null || head.next === null) return head
  const vHead = new ListNode()
  vHead.next = head
  let temp = vHead
  while (head) {
    let end = temp
    for (let i = 0; i < k; i++) {
      end = end.next
      if (end === null) return vHead.next
    }
    const next = end.next
    [head, end] = reverseList(head, end)
    temp.next = head
    end.next = next
    temp = head
    head = end.next
  }
  return vHead.next
}
```
