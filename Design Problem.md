# 设计问题
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

## 380. O(1) 时间插入、删除和获取随机元素
**解题思路**：哈希表和数组，使用一个哈希表来存储每个元素在数组中的下标，也就是将元素值作为键，将下标作为值存储在哈希表中。使用一个数组来存储所有元素，以便支持 O(1) 时间的随机访问。插入元素时，在数组末尾添加新元素，并在哈希表中记录该元素的下标。删除元素时，先从哈希表中获取要删除元素在数组中的下标，将该元素与数组末尾元素交换位置，然后删除末尾元素并更新哈希表中被替换元素的下标。获取随机元素时，生成一个随机数作为数组下标，直接访问该元素即可。
```Python
class RandomizedSet:

    def __init__(self):
        self.nums = []
        self.hash = {}

    def insert(self, val: int) -> bool:
        if val in self.hash:
            return False
        self.hash[val] = len(self.nums)
        self.nums.append(val)
        return True

    def remove(self, val: int) -> bool:
        if val not in self.hash:
            return False
        index = self.hash[val]
        self.nums[index] = self.nums[-1]
        self.hash[self.nums[index]] = index
        self.nums.pop()
        del self.hash[val]
        return True

    def getRandom(self) -> int:
        return choice(self.nums)


# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```
