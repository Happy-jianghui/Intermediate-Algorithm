# 数学
## 297.二叉树的序列化与反序列化
**解题思路**：题解：二叉树的序列化与反序列化是指将一棵二叉树序列化为字符串，再将该字符串反序列化为原来的二叉树。这种技术在数据存储、网络传输等方面有很广泛的应用。对于 serialize 方法，我们使用层次遍历的方式遍历二叉树，将节点的值加入一个字符串数组中，如果节点为 None，我们就将 "null" 字符串加入数组中。最后将这个数组转化为一个字符串，并返回。
对于 deserialize 方法，我们首先将字符串中的值分离出来，存储到一个数组 vals 中。然后我们创建一个根节点，将其加入到队列中。接下来，我们使用层次遍历的方式遍历字符串中的节点值，对于每个值，如果其不是 "null"，我们就创建一个节点，并将其加入到当前节点的左子树或右子树上，同时将其加入队列中。最后返回根节点，就得到了反序列化后的二叉树。
```Python
class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root: return "[]"
        queue = collections.deque()
        queue.append(root)
        res = []
        while queue:
            node = queue.popleft()
            if node:
                res.append(str(node.val))
                queue.append(node.left)
                queue.append(node.right)
            else:
                res.append("null")
        return '[' + ',' . join(res) + ']'
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if data == "[]": return
        vals, i = data[1:-1].split(','), 1
        root = TreeNode(int(vals[0]))
        queue = collections.deque()
        queue.append(root)
        while queue:
            node = queue.popleft()
            if vals[i] != "null":
                node.left = TreeNode(int(vals[i]))
                queue.append(node.left)
            i += 1
            if vals[i] != "null":
                node.right = TreeNode(int(vals[i]))
                queue.append(node.right)
            i += 1
        return root
```
