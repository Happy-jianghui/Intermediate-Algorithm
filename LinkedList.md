# 链表
## 2.两数相加
**解题思路**：将两个数的每一位相加，从最低位开始相加，若有进位则将进位加到下一位的计算中，继续到最高位为止，
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
