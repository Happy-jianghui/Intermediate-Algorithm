# 链表
## 2.两数相加
**解题思路**：将两个数的每一位相加，从最低位开始相加，若有进位则将进位加到下一位的计算中，继续到最高位为止。
```Python
def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        add = 0
        cur = dummy = ListNode()

        while l1 or l2 or add:
            add += (l1.val if l1 else 0) + (l2.val if l2 else 0)
            cur.next = ListNode(add % 10)
            add //= 10
            cur = cur.next
            l1 = l1.next if l1 else 0
            l2 = l2.next if l2 else 0
        return dummy.next
```

## 328.奇偶链表
**解题思路**：将链表拆分成奇数链表和偶数链表，然后将偶数链表接在奇数链表的后面，形成一个新的链表。
```Python
def oddEvenList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head: 
            return head
        odd_head = head
        even_head = head.next
        odd_node = odd_head
        even_node = even_head

        while even_node and even_node.next:
            odd_node.next = even_node.next
            odd_node = odd_node.next
            even_node.next = odd_node.next
            even_node = even_node.next
        
        odd_node.next = even_head
        return odd_head
```

## 160.相交链表
**解题思路**：同时遍历链表A和链表B，当遍历到链表末尾时，将指针指向另一个链表的头部，这样当两个链表长度差为 k 时，它们会同时到达交点。如果没有交点，两个指针最终都会指向 None，返回 None 即可。
```Python
def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        A, B = headA, headB

        while A != B:
            A = A.next if A else headB
            B = B.next if B else headA
        return A
```
