# 动态规划
## 55.跳跃游戏
**解题思路**：荷兰国旗问题，三指针，初始化三个指针i、j和cur，i指向开头位置，j指向结尾位置，cur从头开始遍历数组。当cur指针指向0时，交换cur和i指针所在位置的元素，同时将i和cur指针都向右移动一位。当cur指针指向2时，交换cur和j指针所在位置的元素，同时将j指针向左移动一位。当cur指针指向1时，不需要任何操作，直接将cur指针向右移动一位。遍历结束后，数组中的元素就已经按照红色、白色、蓝色的顺序排列好了
```Python
def sortColors(self, nums: List[int]) -> None:
        i, cur, j = 0, 0, len(nums) - 1
        while cur <= j:
            if nums[cur] == 0:
                nums[cur], nums[i] = nums[i], nums[cur]
                cur += 1
                i += 1
            elif nums[cur] == 2:
                nums[cur], nums[j] = nums[j], nums[cur]
                j -= 1
            else:
                cur += 1
```
