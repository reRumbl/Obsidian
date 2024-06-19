**TensorFlow** – это библиотека машинного обучения с открытым исходным кодом, разработанная компанией Google Brain (исследовательское подразделение Google) для создания и обучения разнообразных моделей машинного обучения.

![[TensorFlow.png]]

**Установка через cmd или terminal:**

```Python
pip install tensorflow
```

**Подключение в проект:**

```Python
import tensorflow
```

**Построение базовой нейронной сети на TensoFlow:**

```Python
(train_images, train_labels), (test_images, test_labels) = mnist.load_data() train_images = train_images.reshape((60000, 28 * 28))
train_images = train_images.astype("float32") / 255
test_images = test_images.reshape((10000, 28 * 28))
test_images = test_images.astype("float32") / 255

model = keras.Sequential([
	layers.Dense(512, activation="relu"),
	layers.Dense(10, activation="softmax")
])
```

