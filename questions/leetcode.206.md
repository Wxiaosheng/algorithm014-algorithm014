## LeetCode 206 反转链表(使用递归模板改写)
反转一个单链表。

    示例:

    输入: 1->2->3->4->5->NULL
    输出: 5->4->3->2->1->NULL

进阶: 你可以迭代或递归地反转链表。你能否用两种方法解决这道题？  

#### 方法一、迭代
借助两个指针，每次只反转当前的结点，并且保存反转过的链表

```javascript
var reverseList = function (head) {
    if (head == null || head.next == null) return head

    let prev = null
    while (head !== null) {
        const next = head.next
        head.next = prev
        prev = head
        head = next
    }   
    return prev 
}
```

#### 方法二、迭代
LeetCode 中比较简洁的回答
```javascript
var reverseList = function (head) {
    if (head == null || head.next == null) return head
    const next = reverseList(head.next)
    head.next.next = head
    head.next = null
    return next
}
```

通过学习递归，了解了递归的四步拆解方法

```javascript
var reverseList = function (head) {
    const helper = function (prev, head) {
        // terminator
        if (head == null) return prev
        // proess current logic
        const next = head.next
        head.next = prev
        prev = head
        // drill down
        return helper(prev, next)
        // restore
    }
    return helper(null, head)
}
```