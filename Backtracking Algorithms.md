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
