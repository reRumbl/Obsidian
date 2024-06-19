В [[PyTorch|PyTorch]] для создания нейронных сетей используется [[Классы|класс]] **nn.Module**. Этот [[Классы|класс]] предоставляет базовую инфраструктуру для определения слоев нейронной сети и методов их использования.

**Пример простой нейронной сети на PyTorch:**

```Python
import torch
from torch import nn

class NeuralNetwork(nn.Module):
    def __init__(self):
        super(NeuralNetwork, self).__init__()
        self.fc1 = nn.Linear(3, 3, dtype=torch.float32)

    def forward(self, x):
        x = self.fc1(x)
        return x

model = NeuralNetwork()

# Генерация случайного тензора с использованием PyTorch
input_tensor = torch.rand(3, dtype=torch.float32) * 10  # случайные значения от 0 до 10
print(f'Input: {input_tensor}')

output_tensor = model(input_tensor)
print(f'Output: {output_tensor}')
```




