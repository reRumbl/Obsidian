Простая [[Сверточные нейронные сети|сверточная нейронная сеть]] в [[TensorFlow#^8b88d6|TensorFlow]] это стек слоев Conv2D и MaxPooling2D.

Слой Conv2D получает следующие параметры: `Conv2D(выходная_глубина, (высота_окна, ширина_окна))`.

**Пример сверточной нейронной сети распознавания изображений MNIST:**

```Python  
from tensorflow import keras

inputs = keras.Input(shape=(28, 28, 1))  
x = keras.layers.Conv2D(filters=32, kernel_size=3, activation='relu')(inputs)  
x = keras.layers.MaxPooling2D(pool_size=2)(x)  
x = keras.layers.Conv2D(filters=64, kernel_size=3, activation='relu')(x)  
x = keras.layers.MaxPooling2D(pool_size=2)(x)  
x = keras.layers.Conv2D(filters=128, kernel_size=3, activation='relu')(x)  
x = keras.layers.Flatten()(x)  
outputs = keras.layers.Dense(10, activation='softmax')(x)  
  
model = keras.Model(inputs=inputs, outputs=outputs, name='MNISTConvClassificator')  
```

При использовании слоев Conv2D [[Сверточные нейронные сети#^6cf30d|дополнение]] настраивается с помощью аргумента `padding`, который принимает два значения: `"valid"`, означающее отсутствие дополнения (будут использоваться только допустимые местоположения окна), и `"same"`, означающее «дополнить так, чтобы выходная карта признаков имела те же ширину и высоту, что и входная». По умолчанию аргумент padding получает значение `"valid"`.

## Оптимизация сверточной сети на примере

Для примера возьмем сверточную нейронную сеть для бинарной классификации собак/кошек.

**Имеем следующую модель:**\

```Python
inputs = keras.Input(shape=(180, 180, 3)) 
x = keras.layers.Rescaling(1./255)(inputs)
x = keras.layers.Conv2D(filters=32, kernel_size=3, activation='relu')(x)  
x = keras.layers.MaxPooling2D(pool_size=2)(x)  
x = keras.layers.Conv2D(filters=64, kernel_size=3, activation='relu')(x)  
x = keras.layers.MaxPooling2D(pool_size=2)(x)  
x = keras.layers.Conv2D(filters=128, kernel_size=3, activation='relu')(x)  
x = keras.layers.MaxPooling2D(pool_size=2)(x)  
x = keras.layers.Conv2D(filters=256, kernel_size=3, activation='relu')(x)  
x = keras.layers.MaxPooling2D(pool_size=2)(x)  
x = keras.layers.Conv2D(filters=256, kernel_size=3, activation='relu')(x)  
x = keras.layers.Flatten()(x)  
outputs = keras.layers.Dense(1, activation='sigmoid')(x)
  
model = keras.Model(inputs=inputs, outputs=outputs, name='dogsvscats')
```

Изначально модель достигает точности ~70%, после чего начинается [[Переобучение, способы борьбы с ним|переобучение]]. Для борьбы с [[Переобучение, способы борьбы с ним|переобучением]] можно использовать [[Переобучение, способы борьбы с ним#^66422a|обогащение данных]], для этого следует добавить несколько слоев обогащения в начале модели.

**Пример этапа обогащения данных:**

```Python
data_augmentation = keras.Sequential([
	layers.RandomFlip('horizontal'), 
	layers.RandomRotation(0.1), 
	layers.RandomZoom(0.2)
])
```

*Подробно о слоях:*

- `RandomFlip('horizontal')` — переворачивает по горизонтали 50 % случайно выбранных изображений.

- `RandomRotation(0.1)` — поворачивает входные изображения на случайный угол в диапазоне [–10 %, +10 %] (параметр определяет долю полной окружности — в градусах заданный здесь диапазон составит [–36, +36]).

- `RandomZoom(0.2)` — случайным образом изменяет масштаб изображения, в данном случае в диапазоне [–20 %, +20 %].

И последнее, что следует знать о слоях обогащения изображений случайными преобразованиями: так же как `Dropout`, они неактивны на этапе прогнозирования (когда вызывается метод `predict()` или `evaluate()`). Во время оценки модель будет вести себя так, как если бы мы не задействовали [[Переобучение, способы борьбы с ним#^ee82d2|прореживание]] и [[Переобучение, способы борьбы с ним#^66422a|обогащение данных]].

Продолжая борьбу с [[Переобучение, способы борьбы с ним|переобучением]], добавим в модель слой `Dropout`, непосредственно перед полносвязным классификатором, который будет выполнять [[Переобучение, способы борьбы с ним#^ee82d2|прореживание]].

**Модель с прореживанием и обогащением:**

```Python

```