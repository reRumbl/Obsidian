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

**Пример базовой нейронной сети для классификации изображений из набора данных MNIST:**

```Python
import torch  
from torch import nn  
from torchvision import datasets, transforms  
from torch.utils.data import DataLoader  
import torch.optim as optim  
  
  
class MNISTClassification(nn.Module):  
    def __init__(self):  
        super(MNISTClassification, self).__init__()  
        self.conv1 = nn.Conv2d(1, 32, kernel_size=3, stride=1, padding=1)  
        self.conv2 = nn.Conv2d(32, 64, kernel_size=3, stride=1, padding=1)  
        self.pool = nn.MaxPool2d(kernel_size=2, stride=2, padding=0)  
        self.flatten = nn.Flatten()  
        self.fc1 = nn.Linear(64 * 7 * 7, 128)  
        self.fc2 = nn.Linear(128, 64)  
        self.fc3 = nn.Linear(64, 10)  
        self.relu = nn.ReLU()  
        self.loss_func = None  
        self.optimizer = None  
  
    def forward(self, x):  
        x = self.pool(self.relu(self.conv1(x)))  
        x = self.pool(self.relu(self.conv2(x)))  
        x = self.flatten(x)  
        x = self.relu(self.fc1(x))  
        x = self.relu(self.fc2(x))  
        x = self.fc3(x)  
        return x  
  
    def fit(self, train_loader, val_loader, epochs=100):  
        self.loss_func = nn.CrossEntropyLoss()  
        self.optimizer = optim.Adam(self.parameters(), lr=0.001)  
        device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')  
        self.to(device)  
  
        for epoch in range(epochs):  
            self.train()  
            epoch_loss = 0.0  
            correct = 0  
            total = 0  
  
            for images, labels in train_loader:  
                images, labels = images.to(device), labels.to(device)  
                outputs = self(images)  
                loss = self.loss_func(outputs, labels)  
  
                self.optimizer.zero_grad()  
                loss.backward()  
                self.optimizer.step()  
  
                epoch_loss += loss.item()  
                _, predicted = torch.max(outputs.data, 1)  
                total += labels.size(0)  
                correct += (predicted == labels).sum().item()  
  
            avg_loss = epoch_loss / len(train_loader)  
            accuracy = 100 * correct / total  
            print(f'Epoch {epoch + 1}/{epochs}, Loss: {avg_loss:.4f}, Accuracy: {accuracy:.2f}%')  
  
            self.validate(val_loader, device)  
  
    def validate(self, val_loader, device):  
        self.eval()  
        val_loss = 0.0  
        correct = 0  
        total = 0  
  
        with torch.no_grad():  
            for images, labels in val_loader:  
                images, labels = images.to(device), labels.to(device)  
                outputs = self(images)  
                loss = self.loss_func(outputs, labels)  
                val_loss += loss.item()  
                _, predicted = torch.max(outputs.data, 1)  
                total += labels.size(0)  
                correct += (predicted == labels).sum().item()  
  
        avg_val_loss = val_loss / len(val_loader)  
        val_accuracy = 100 * correct / total  
        print(f'Validation Loss: {avg_val_loss:.4f}, Validation Accuracy: {val_accuracy:.2f}%')  
  
  
transform = transforms.Compose([  
    transforms.ToTensor(),  
    transforms.Normalize((0.5,), (0.5,))  
])  
  
train_dataset = datasets.MNIST(root='./data', train=True, transform=transform, download=True)  
train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)  
  
val_dataset = datasets.MNIST(root='./data', train=False, transform=transform, download=True)  
val_loader = DataLoader(val_dataset, batch_size=32, shuffle=False)  
  
model = MNISTClassification()  
model.fit(train_loader, val_loader,  epochs=5)
```


