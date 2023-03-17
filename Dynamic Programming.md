# 动态规划
## 55.跳跃游戏
**解题思路**：维护一个变量res，表示在当前位置之前，能够到达的最远距离。我们遍历数组nums，对于每一个位置i，如果res >= i，表示当前位置之前能够到达，再加上i位置上的跳跃步数num，就能够到达i+num位置。如果i+num的值比res还大，就更新res为i+num。最后判断res是否大于等于数组最后一个位置n-1即可。
```Python
def canJump(self, nums: List[int]) -> bool:
        res = 0
        for i, num in enumerate(nums):
            if res >= i and i + num > res:
                res = i + num
        return res >= i
```


## 62.不同路径
**解题思路**：动态规划思路，初始化值为1，可以省略赋值，上方的值+左方的值 = 当前的值
```Python
def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1 for _ in range(n)] for _ in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i][j-1] + dp[i-1][j]
        return dp[-1][-1]
```

## 322.零钱兑换
**解题思路**：动态规划思路，没看懂，先搬运大神的代码
```Python
def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] * (amount+1)
        dp[0] = 0
        
        for i in range(1, amount+1):
            for coin in coins:
                if coin <= i:
                    dp[i] = min(dp[i], dp[i-coin] + 1)
        return dp[amount] if dp[amount] != float('inf') else -1
```
