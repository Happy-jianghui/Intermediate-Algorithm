# 排序和搜索
## 75.颜色分类
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

## 347.前K个高频元素
**解题思路**：使用了Python中的内置函数sorted()来对哈希表中的项按值进行排序，并通过lambda函数指定按值进行排序，并设置reverse参数为True来实现降序排序。然后使用for循环从排序后的哈希表中取出前k个元素，并将其键加入结果列表中。
```Python
def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        hash = {}
        for num in nums:
            if num not in hash:
                hash[num] = 1
            else:
                hash[num] += 1
        hash = sorted(hash.items(), key = lambda x:x[1], reverse = True)
        res = []
        for i in range(k):
            res.append(hash[i][0])
        return res
```

## 215.数组中的第K个最大元素
**解题思路**：通过快速选择算法找到数组中的第k个最大元素
```Python
def findKthLargest(self, nums: List[int], k: int) -> int:
        left, right, target = 0, len(nums) - 1, k - 1
        while True:
            pivotIndex  = self.partition(nums, left, right)
            if pivotIndex  == target:
                return nums[pivotIndex ]    
            elif pivotIndex  > k: #要往左找
                right = pivotIndex  - 1
            elif pivotIndex  < k: #要往右找
                left = pivotIndex  + 1
                
    def partition(self, nums, left, right):
        import random
        k = random.randint(left, right)
        pivot = nums[k]
        nums[left], nums[k] = nums[k], nums[left]
        index = left
        
        for i in range(left + 1, right + 1):
            if nums[i] > pivot:
                index += 1
                nums[i], nums[index] = nums[index], nums[i]
        nums[left], nums[index] = nums[index], nums[left]
        return index #此时所有index左侧的值都比nums[index]大， 所有右侧的值都比nums[index]小
```

## 162.寻找峰值
**解题思路**：二分查找，每次可以通过比较中间位置 `mid` 和 `mid+1` 的值，来判断峰值在左侧还是右侧。如果 `nums[mid] > nums[mid+1]`，则峰值可能在左侧，否则峰值可能在右侧。
```Python
def findPeakElement(self, nums: List[int]) -> int:
        n = len(nums)
        left, right = 0, n-1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] > nums[mid + 1]:
                right = mid
            else:
                left = mid + 1
        return left
```
