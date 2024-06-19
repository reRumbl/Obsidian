В [[PyTorch|PyTorch]] для создания нейронных сетей используется [[Классы|класс]] **nn.Module**. Этот [[Классы|класс]] предоставляет базовую инфраструктуру для определения слоев нейронной сети и методов их использования.

**Пример простой нейронной сети на PyTorch:**

```Python
import torch.nn as nn

# Определение нейронной сети на основе nn.Module
class SimpleNN(nn.Module):
    def __init__(self):
        super(SimpleNN, self).__init__()
        self.fc1 = nn.Linear(3, 3)  # Полносвязный слой (fully connected layer)

    def forward(self, x):  # Переопределение метода forward()
        x = self.fc1(x)
        return x

# Создание экземпляра модели
model = SimpleNN()

# Пример ввода
input_tensor = torch.tensor([1.0, 2.0, 3.0])
output_tensor = model(input_tensor)
print("Output:", output_tensor)
```


