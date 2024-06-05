Binar Tree - структура данных, элементы которой хранят значение и две ссылки на правый и левый дочерние элементы.

**Реализация при помощи двух [[Классы|классов]]:**

```Python
class TreeNode:
	def __init__(self, value=0, left=None, right=None):
		self.value = value
		self.left = left
		self.right = right


class BinarTree:
	def __init__(self, root=TreeNode()):
		self.root = root
```

**Пример экземпляра:**

```Python
nodell = TreeNode(7)
nodelr = TreeNode(3)
nodel = TreeNode(4, nodell, nodelr)

noderl = TreeNode(5)
noderr = TreeNode(1)
noder = TreeNode(2, noderl, noderr)

root = TreeNode(6, nodel, noder)
tree = BinarTree(root)
```

*Схематичное изображение данного экземпляра:*

![[Классический BinarTree.png]]