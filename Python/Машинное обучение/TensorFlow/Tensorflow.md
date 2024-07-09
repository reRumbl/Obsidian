**TensorFlow** – это библиотека машинного обучения для [[Python|Python]] с открытым исходным кодом, разработанная компанией Google Brain (исследовательское подразделение Google) для создания и обучения разнообразных моделей машинного обучения.

![[TensorFlow.png]]

**Установка через cmd или terminal:**

```Python
pip install tensorflow
```

**Подключение в проект:**

```Python
import tensorflow
```
## Keras

Глубокое обучение в **TensorFlow** реализуется через библиотеку **Keras**. **Keras** — это библиотека глубокого обучения для [[Python|Python]], основанная на **TensorFlow**, которая обеспечивает удобный способ определения и тренировки моделей глубокого обучения. Первоначально **Keras** создавалась для исследований с целью упростить эксперименты с глубоким обучением.

![[Keras.png]]

**Построение и обучение базовой нейронной сети на TensorFlow:**

```Python
(train_images, train_labels), (test_images, test_labels) = mnist.load_data() train_images = train_images.reshape((60000, 28 * 28))
train_images = train_images.astype("float32") / 255
test_images = test_images.reshape((10000, 28 * 28))
test_images = test_images.astype("float32") / 255

model = keras.Sequential([
	layers.Dense(512, activation="relu"),
	layers.Dense(10, activation="softmax")
])

model.compile(optimizer="rmsprop", loss="sparse_categorical_crossentropy", metrics=["accuracy"])

model.fit(train_images, train_labels, epochs=5, batch_size=128)
```
