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

## 103.二叉树的锯齿形层序遍历
**解题思路**：使用 BFS 遍历二叉树时，可以按照层次遍历的方式遍历每一层节点，然后再根据深度的奇偶性来判断是正序还是倒序。
```Python
def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        queue = collections.deque()
        queue.append(root)
        res = []
        deepth = 1

        while queue:
            tmp = []
            for _ in range(len(queue)):
                node = queue.popleft()
                tmp.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            if deepth % 2 == 0:
                res.append(tmp[::-1])
            else:
                res.append(tmp)
            deepth += 1
        return res  
```


## 105.从前序与中序遍历序列构造二叉树
**解题思路**：递归
```Python
def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not (preorder and inorder):
            return None
        
        root = TreeNode(preorder[0])
        mid_idx = inorder.index(preorder[0])

        root.left = self.buildTree(preorder[1:mid_idx+1], inorder[:mid_idx+1])
        root.right = self.buildTree(preorder[mid_idx+1:], inorder[mid_idx+1:])
        return root
```

## 116.填充每个节点的下一个右侧节点指针
**解题思路**：层次遍历二叉树的方式解决，注意遍历当前层的节点，对于每个节点： i. 如果该节点有左儿子和右儿子，将左儿子的 next 指针指向右儿子，并将右儿子的 next 指针指向该节点的 next 节点的左儿子（如果存在），然后将左右儿子放入队列中，处理下一个节点。
```Python
def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if not root:
            return root
        queue = collections.deque()
        queue.append(root)

        while queue:
            n = len(queue)
            for i in range(len(queue)):
                node = queue.popleft()
                if i < len(queue) - 1:
                    node.next = queue[0]
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        return root
```

## 230.二叉搜索树中第k小的元素
**解题思路**：中序遍历，遍历到一个节点时，将计数器k减1，代表已经遍历了一个节点。如果k值已经减为0，说明当前节点是二叉搜索树中的第K小节点，将该节点的值记录在变res中。
```Python
def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if not root:
            return root
        queue = collections.deque()
        queue.append(root)

        while queue:
            n = len(queue)
            for i in range(len(queue)):
               node = queue.popleft()
                if i < len(queue) - 1:
                    node.next = queue[0]
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        return root
```

## 200.岛屿数量
**解题思路**：定义一个计数器`count`，用来记录岛屿的数量, 遍历二维网格中的每个元素，如果当前元素是陆地（值为1），则从该元素开始使用DFS遍历相邻的陆地，并将遍历到的陆地都标记为已访问（值为）,遍历完一个岛屿后，将计数器`count`加1,继续遍历其他元素，直到遍历完整个二维网格。最后返回计数器`count`，即为岛屿的数量。
```Python
def numIslands(self, grid: List[List[str]]) -> int:
        def dfs(i, j):
            if i < 0 or j < 0 or i >= len(grid) or j >= len(grid[0]) or grid[i][j] != '1':
                return
            grid[i][j] = '2'
            dfs(i-1, j)
            dfs(i+1, j)
            dfs(i, j-1)
            dfs(i, j+1)
        
        if not grid:
            return 0
        count = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] ==  "1":
                    dfs(i, j)
                    count += 1
        return count
```
