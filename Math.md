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

## 172.阶乘后的零
**解题思路**：利用因子分解的思想，因为末尾的零是由因子 2 和因子 5 相乘得到的，所以我们只需要统计在 n! 的因子中有多少个 5 即可。
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

## 171.Excel表列序号
**解题思路**：每个字母所代表的数字可以通过将其 ASCII 码减去 64（即 'A' 的 ASCII 码减去 1）得到，然后根据列名的位数，按照 26 进制进行累加。
```Python
def titleToNumber(self, columnTitle: str) -> int:
        res = 0
        for i in columnTitle:
            res = res * 26 + ord(i) - 64
        return res
```

## 50.Pow(x,n)
**解题思路**：先检查 n 是否小于 0，如果是，则将 x 变为 1/x ，并将 n 取反以确保 n 为正数。接下来，使用循环和位运算来计算 x^n的值，并返回最终的结果。
```Python
def myPow(self, x: float, n: int) -> float:
        if n < 0:
            x = 1/x
            n = -n
        res = 1
        while n > 0:
            if n % 2 == 1:
                res *= x
            x *= x
            n //= 2
        return res
```
