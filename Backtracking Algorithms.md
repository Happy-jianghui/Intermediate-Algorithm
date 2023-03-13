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
