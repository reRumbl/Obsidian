**Тензоры в PyTorch** — это обобщение массивов и матриц. Они могут быть использованы для представления многомерных данных. [[PyTorch|PyTorch]] поддерживает множество операций над тензорами, аналогичных тем, которые можно выполнять с массивами в [[NumPy|NumPy]].

**Пример работы с тензорами в PyTorch:**

```Python
import torch

a = torch.tensor([1.0, 2.0, 3.0])
b = torch.tensor([4.0, 5.0, 6.0])

c = a + b
d = a * b
e = torch.dot(a, b)
```

**Сложение тензоров:**

```Python
a = torch.tensor([1.0, 2.0, 3.0])
b = torch.tensor([4.0, 5.0, 6.0])

c = a + b
```

**Поэлементное умножение тензоров:**

```Python
a = torch.tensor([1.0, 2.0, 3.0])
b = torch.tensor([4.0, 5.0, 6.0])

c = a * b
```

**Матричное умножение тензоров, имеющих 1 измерение:**

```Python
a = torch.tensor([1.0, 2.0, 3.0])
b = torch.tensor([4.0, 5.0, 6.0])

c = torch.dot(a, b)
```

**Матричное умножение тензоров, имеющих любое количество измерений:**

```Python
a = torch.tensor([1.0, 2.0, 3.0])
b = torch.tensor([4.0, 5.0, 6.0])

c = torch.matmul(a, b)
```

**Нахождение суммы элементов тензора:**

```Python
a = torch.tensor([1.0, 2.0, 3.0])
print(a.sum())
```

**Создание тензоров указанной размерности со случайными значениями:**

```Python
rand_tensor = torch.rand(3, dtype=torch.float32) * 10  # Случайные значения от 0 до 10

randn_tensor = torch.randn((7, 3)) # Случайные значения из нормального распределения

randint_tensor = torch.randint(0, 255, (4, 9))  # Случайные целые числа в диапазоне
```

**Создание тензоров указанной размерности со случайными значениями через NumPy:**

```Python
import numpy as np

a = torch.tensor(np.random.random((3, 3)), dtype=torch.float32)
b = torch.tensor(np.random.uniform(0.0, 10.0, (3, 3)), dtype=torch.float32)
```




