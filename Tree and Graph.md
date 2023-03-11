# 树和图
## 2.二叉树的中序遍历
**解题思路**：中序遍历 左节点-> 根 -> 右节点，可用递归或栈实现
```Python
#递归
def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []

        def dfs(root):
            if not root:
                return
            dfs(root.left)
            res.append(root.val)
            dfs(root.right)
        dfs(root)
        return res
#栈
def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        stack = []

        while stack or root:
            if root:
                stack.append(root)
                root = root.left
            else:
                tmp = stack.pop()
                res.append(tmp.val)
                root = tmp.right
        return res
```
