Связный список - структура данных, элементы которой хранят значение и ссылку на следующий элемент.

**Реализация при помощи двух [[Классы|классов]]:**

```Python
class ListNode:  
    def __init__(self, value=None, next_node=None):  
        self.value = value  
        self.next_node = next_node  
  
  
class LinkedList:  
    def __init__(self, head=None):  
        self.head = head
```

**Пример экземпляра:**

```Python
node3 = ListNode(4)
node2 = ListNode(3, node3)
node1 = ListNode(2, node2)
nodehead = ListNode(1, node1)
data = LinkedList(nodehead)
```

*Схематичное изображение данного экземпляра:*

*![[Цикличный Linked List.png]]

