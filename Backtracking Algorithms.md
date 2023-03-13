# 回溯算法
## 17.电话号码的字母组合
**解题思路**：使用递归函数dfs来生成所有的字母组合。在递归函数中，用index来记录当前处理的数字下标，用path来记录当前已生成的字母组合。在递归终止时，将当前path添加到结果列表中。
```Python
#递归
def letterCombinations(digits) -> str:
    if not digits:
        return []
    # 定义数字到字母的映射关系
    phone_map = {
        '2': 'abc',
        '3': 'def',
        '4': 'ghi',
        '5': 'jkl',
        '6': 'mno',
        '7': 'pqrs',
        '8': 'tuv',
        '9': 'wxyz'
    }
    # 定义递归函数ffff
    def dfs(index, path):
        # 递归终止条件：当处理到最后一个数字时，将当前路径添加到结果中，并返回
        if index == len(digits):
            res.append(path)
            return
        # 获取当前数字对应的字母集合
        letters = phone_map[digits[index]]

        # 依次尝试每一个字母，并递归处理下一个数字
        for letter in letters:
            dfs(index + 1, path + letter)

    res = []
    dfs(0, "")
    return res

print(letterCombinations('23'))

#迭代
def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []

        map = {
            '2': 'abc',
            '3': 'def',
            '4': 'ghi',
            '5': 'jkl',
            '6': 'mno',
            '7': 'pqrs',
            '8': 'tuv',
            '9': 'wxyz'
        }

        res = ['']
        for digit in digits:
            letters = map[digit]
            tmp_res = []
            for letter in letters:
                for s in res:
                    tmp_res.append(s + letter)
            res = tmp_res
        
        return res
```

## 22.括号生成
**解题思路**：定义一个字符串变量，用于保存正在生成的括号序列。定义两个计数器变量left和right，分别表示当前已经添加的左括号数和右括号数。如果left和right的值都等于n，将当前的括号序列添加到结果列表中。如果left小于n，则在当前括号序列后面加上左括号，并递归调用自身。如果在添加左括号之前，已经添加的左括号数大于右括号数，则在当前括号序列后面加上右括号，并递归调用自身。
```Python
def generateParenthesis(self, n: int) -> List[str]:
        def dfs(path, left, right):
            if left == n and right == n:
                res.append(path)
                return
            if left < right:
                return 
            if left < n:
                dfs(path+'(', left+1, right)
            if right < n:
                dfs(path+')', left, right+1)
        res = []
        dfs('', 0, 0)
        return res
```

## 46.全排列
**解题思路**：这是一个用于求解给定列表 nums 的全排列的深度优先搜索(DFS)算法。算法中的 dfs() 是一个递归函数，它对每个未被标记为使用过的数字进行取数操作，并将其添加到当前路径中，然后递归调用 dfs() 函数继续处理下一层的数字。当深度等于给定列表的长度时，说明已经找到了一组全排列，将其添加到结果列表 res 中。在返回上一层之前，需要将该数字从当前路径 path 中弹出并将其标记为未使用过，以便在后续的搜索中可以重复使用。
```Python
def permute(self, nums: List[int]) -> List[List[int]]:
        def dfs(depth, path, used):
            if depth == len(nums):
                res.append(path[:])
            for i in range(len(nums)):
                if not used[i]:
                    used[i] = True
                    path.append(nums[i])
                    dfs(depth+1, path, used)
                    used[i] = False
                    path.pop()
        res = []
        used = [False for _ in range(len(nums))]
        dfs(0, [], used)
        return res
```

## 46.子集
**解题思路**：初始化两个空数组 path 和 res，分别用于存储当前正在访问的子集和所有生成的子集。定义递归函数 recur(nums, i)，其中 nums 表示当前正在处理的数组，i 表示当前位置的索引。在递归函数中先将当前子集加入到结果数组 res 中。然后判断当前位置是否超出数组范围，如果是就直接返回。枚举当前位置后面的元素，将元素加入到当前子集 path 中，并递归处理下一个位置。递归回溯时，需要将刚才加入的元素从 path 中弹出，以便处理上一层的状态。在主函数中调用 recur(nums, 0)，从第一个位置开始枚举，得到所有的子集后返回结果数组 res。
```Python
def subsets(self, nums: List[int]) -> List[List[int]]:
        path = []
        res = []

        def recur(nums, i):
            res.append(path[:])
            if i >= len(nums):
                return

            for j in range(i, len(nums)):
                path.append(nums[j])
                recur(nums, j+1)
                path.pop()

        recur(nums, 0)
        return res
```
