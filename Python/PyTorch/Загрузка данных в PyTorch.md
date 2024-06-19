[[PyTorch|PyTorch]] предоставляет удобные [[Классы|классы]] для работы с наборами и загрузкой данных. **torchvision.datasets** включает в себя популярные наборы данных для обучения моделей, а **torch.utils.data.DataLoader** помогает загружать данные небольшими порциями (пакетами).

**Пример использования DataLoader:**

```Python
import torch
from torchvision import datasets, transforms
from torch.utils.data import DataLoader

# Трансформации для предобработки данных
transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))
])

# Загрузка датасета MNIST
train_dataset = datasets.MNIST(root='./data', train=True, transform=transform, download=True)
train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)

# Пример итераций по DataLoader
for images, labels in train_loader:
    print(images.shape, labels.shape)
```