# 数组和字符串
## 15.三数之和
**解题思路**：双指针，首先对数组进行排序，然后依次遍历数组中的每个数。对于每个数，我们使用双指针来查找另外两个数，使它们的和等于目标值。注意：在查找的过程中，需要跳过重复的数字
```Python
def threeSum(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        res = []
        nums.sort()

        for i in range(n):
            if i > 0 and nums[i] == nums[i-1]: continue
            left, right = i+1, n-1
            while left < right:
                sum = nums[i] + nums[left] +nums[right]
                if sum == 0:
                    res.append([nums[i], nums[left], nums[right]])
                    while left < right and nums[left] == nums[left+1]:
                        left += 1
                    while left < right and nums[right] == nums[right-1]:
                        right -= 1
                    left += 1
                    right -= 1
                elif sum > 0:
                    right -= 1
                else:
                    left += 1
        return res
```
