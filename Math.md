# 数学
## 202.快乐数
**解题思路**：快慢指针，定义两个指针 slow 和 fast，初始时都指向输入的整数 n。在循环中，slow 每次计算各位数字的平方和并将结果赋值给自己，即 slow = getnum(slow)。而 fast 则每次计算两次各位数字的平方和，并将结果赋值给自己，即 fast = getnum(getnum(fast))。如果输入的数是快乐数，则快慢指针最终会相遇在 1 处；如果不是快乐数，则快指针会进入一个循环，此时 slow 和 fast 最终会相遇在循环内的某个位置。在循环中，如果 slow == fast，则说明两个指针相遇，返回 True；否则继续执行调用快慢函数。
```Python
def isHappy(self, n: int) -> bool:
        def getnum(num):
            sum = 0
            while num > 0:
                digit = num % 10
                sum += (digit**2)
                num //= 10
            return sum
        slow, fast = n, n
        while True:
            slow = getnum(slow)
            fast = getnum(getnum(fast))
            if fast == 1:
                return True
            elif fast == slow:
                return False
```
