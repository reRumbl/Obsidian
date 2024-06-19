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

	def fit(self, x_train, x_labels, epochs=100):  
    self.loss_func = nn.CrossEntropyLoss()  
    self.optimizer = optim.Adam(self.parameters(), lr=0.001)  
  
    for epoch in range(epochs):  
        epoch_loss = 0.0  
  
        for i in range(x_train.size(0)):  
            # Прямой проход  
            outputs = self(x_train[i])  
  
            # Вычисление потерь  
            loss = self.loss_func(outputs.unsqueeze(0), x_labels[i].unsqueeze(0))  
  
            # Обратное распространение  
            self.optimizer.zero_grad()  
            loss.backward()  
  
            # Обновление параметров  
            self.optimizer.step()  
  
            epoch_loss += loss.item()  
  
        # Средние потери за эпоху  
        epoch_loss /= x_train.size(0)  
        print(f'Epoch {epoch + 1}/{epochs}, Loss: {epoch_loss:.4f}')


model = NeuralNetwork()  
  
# Генерация случайных данных для тренировки  
train_data = torch.rand((10, 3), dtype=torch.float32)  # 10 примеров, 3 входа каждый  
labels = torch.randint(0, 3, (10,), dtype=torch.long)  # 10 меток в диапазоне [0, 3)  
  
# Обучение модели  
model.fit(train_data, labels, epochs=20)
```





