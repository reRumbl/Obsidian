Модель глубокого обучения является графом слоев. В [[TensorFlow#^8b88d6|Keras]] модели представляют собой экземпляры [[Классы|класса]] Model. У Model есть [[Наследование|подклассы]], например последовательные модели Sequential ([[Наследование|подкласс]] [[Классы|класса]] Model) — простой стек слоев, отображающих единственный вход в единственный выход.

**Некоторые виды моделей нейронных сетей:**

- Сети с двумя ветвями (two-branch networks).

- Многоголовые сети (multihead networks).

- Входные блоки (inception blocks).

Выбор правильной архитектуры сети — больше искусство, чем наука. И хотя есть несколько проверенных методов и принципов, на которые можно положиться, только практика может помочь стать опытным архитектором нейронных сетей.

**После того как определена архитектура сети, нужно выбрать еще три параметра:**

- **Функцию потерь (целевую функцию)** — количественную оценку, которая будет минимизироваться в процессе обучения. Представляет собой меру успеха в решении стоящей задачи.

- **Оптимизатор** — определяет, как будет изменяться сеть под воздействием функции потерь. Реализует конкретный вариант стохастического градиентного спуска (Stochastic Gradient Descent, SGD).

- **Метрики** — показатели успеха (такие как точность классификации), за которыми будет вестись наблюдение во время обучения и проверки. Обучение, в отличие от потерь, не оптимизируется по данным показателям напрямую. Поэтому от метрик не требуется, чтобы они были дифференцированными.

## Разные способы создания моделей

В [[TensorFlow#^8b88d6|Keras]] имеется три API для создания моделей: 

- Последовательная модель Sequential, наиболее доступный API — по сути, это список [[Python|Python]], поэтому модели данного вида ограничены простыми наборами слоев; 

- Функциональный API, ориентированный на архитектуры моделей в виде графов. Он представляет собой золотую середину в плане удобства применения и гибкости и поэтому чаще всего используется на практике; 

- Наследование стандартных классов, низкоуровневый способ, который позволяет реализовать все аспекты с нуля. Это идеальный вариант для желающих контролировать каждую мелочь. Однако при выборе данного метода у вас не будет доступа ко многим встроенным функциям [[TensorFlow#^8b88d6|Keras]], а риск допустить ошибку станет выше.

### Последовательная модель Sequential

Самый простой способ создать модель [[TensorFlow#^8b88d6|Keras]] — использовать класс моделей **Sequential**.

**Класс Sequential:**

```Python
from tensorflow import keras
from tensorflow.keras import layers 

model = keras.Sequential([
	layers.Dense(64, activation='relu'), 
	layers.Dense(10, activation='softmax') 
])

# Или

model = keras.Sequential()
model.add(layers.Dense(64, actiavation='relu'))
model.add(layers.Dense(10, activation='softmax'))
```

**Присваивание имен слоям и моделям:**

```Python
model = keras.Sequential(name='my_example_model')
model.add(layers.Dense(64, activation='relu', name='my_first_layer'))
model.add(layers.Dense(10, activation='softmax', name='my_last_layer')) model.build((None, 3))
```

При пошаговом построении модели **Sequential** удобно иметь возможность посмотреть на ее текущее состояние после добавления очередного слоя. Но сводку невозможно получить, пока модель не построена! Эту проблему можно решить, строя модель **Sequential** на лету, для чего достаточно заранее объявить форму входных данных. Это можно сделать с помощью класса Input.

**Предварительное определение формы входных данных модели:**

```Python
model = keras.Sequential() 
model.add(keras.Input(shape=(3,))) 
model.add(layers.Dense(64, activation='relu'))
```

### Функциональный API

Модель Sequential проста в использовании, но круг сфер ее применения чрезвычайно ограничен: она может выражать модели только с одним входом и одним выходом, последовательно применяя слои друг за другом. Но на практике довольно часто встречаются модели с несколькими входами (например, изображение и его метаданные), несколькими выходами (разные признаки, которые необходимо предсказать) или нелинейной топологией. 

В таких случаях модель следует строить с помощью функционального API — именно такой подход для большинства моделей [[TensorFlow#^8b88d6|Keras]] вы встретите в действительности. Это мощный и увлекательный способ конструирования, напоминающий игру с кубиками LEGO.

**Создание простой модели с двумя слоями Dense с помощью функционального API:**

```Python
inputs = keras.Input(shape=(3,), name='my_input')
features = layers.Dense(64, activation='relu')(inputs)
outputs = layers.Dense(10, activation='softmax')(features)
model = keras.Model(inputs=inputs, outputs=outputs)
```

В отличие от этой простой модели большинство моделей глубокого обучения не похожи на списки и скорее напоминают графы. Например, они могут иметь несколько входов или несколько выходов. Именно благодаря таким моделям функциональный API предстает во всем блеске.

**Создание модели с несколькими входами и выходами с помощью функционального API:**

```Python
vocabulary_size = 10000
num_tags = 100
num_departments = 4

title = keras.Input(shape=(vocabulary_size,), name='title')
text_body = keras.Input(shape=(vocabulary_size,), name='text_body')
tags = keras.Input(shape=(num_tags,), name='tag')

features = layers.Concatenate()([title, text_body, tags])
features = layers.Dense(64, activation='relu')(features)
priority = layers.Dense(1, activation='sigmoid', name='priority')(features)
department = layers.Dense(num_departments, activation='softmax', name='department')(features)

model = keras.Model(inputs=[title, text_body, tags], outputs=[priority, department])
```

Обучаются модели с несколькими входами и выходами почти так же, как модели Sequential, — вызовом функции fit() со списками входных и выходных данных. Эти списки должны передаваться в том же порядке, в каком информация о входных данных передавалась конструктору модели. Чтобы не зависеть от конкретного порядка передачи аргументов (например, у вашей модели много входов или выходов и вам не хотелось бы в них запутаться), можно также использовать имена, присвоенные объектам Input и выходным слоям, и передавать данные через словари.

**Обучение такой модели:**

```Python
import numpy as np 

num_samples = 1280

title_data = np.random.randint(0, 2, size=(num_samples, vocabulary_size)) text_body_data = np.random.randint(0, 2, size=(num_samples, vocabulary_size))
tags_data = np.random.randint(0, 2, size=(num_samples, num_tags))

priority_data = np.random.random(size=(num_samples, 1))
department_data = np.random.randint(0, 2, size=(num_samples, num_departments)) 

# Вариант 1 - через списки
model.compile(
	optimizer='rmsprop',
	loss=['mean_squared_error', 'categorical_crossentropy'],
	metrics=[['mean_absolute_error'], ['accuracy']]
)
model.fit(
	[title_data, text_body_data, tags_data], 
	[priority_data, department_data], epochs=1
)
model.evaluate(
	[title_data, text_body_data, tags_data],
	[priority_data, department_data]
)

# Вариант 2 - через словари
model.compile(
	optimizer='rmsprop',
	loss={'priority': 'mean_squared_error', 
		  'department': 'categorical_crossentropy'},
	metrics={'priority': ['mean_absolute_error'], 
			 'department': ['accuracy']}
)
model.fit(
	{'title': title_data, 'text_body': text_body_data, 'tags': tags_data},
	{'priority': priority_data, 'department': department_data}, epochs=1
) 
model.evaluate(
	{'title': title_data, 'text_body': text_body_data, 'tags': tags_data}, 
	{'priority': priority_data, 'department': department_data}
)

priority_preds, department_preds = model.predict([title_data, text_body_data, tags_data])
```

При помощи plot_model() можно сгенерировать графическое представление графа модели. Например, для приведенной выше модели будет сгенерирован следующий граф:

![[Граф модели, сгенерированный при помощи plot_model().png]]

### Создание производных моделей от класса Model

**Подклассы класса Model создаются  следующим образом:**

- В методе `__init__()` определяются слои, которые будет использовать модель.

- В методе `call()` с помощью созданных ранее слоев определяется порядок выполнения прямого прохода модели.

- Создается экземпляр вашего подкласса, после чего ему передаются данные для создания весов

**Пример подкласса Model:**

```Python
class CustomerTicketModel(keras.Model):
	def __init__(self, num_departments):
		super().__init__()
		self.concat_layer = layers.Concatenate()
		self.mixing_layer = layers.Dense(64, activation='relu')
		self.priority_scorer = layers.Dense(1, activation='sigmoid') 
		self.department_classifier = layers.Dense(num_departments, activation='softmax')
	
	def call(self, inputs):
		title = inputs['title']
		text_body = inputs['text_body']
		tags = inputs['tags']
		
		features = self.concat_layer([title, text_body, tags])
		features = self.mixing_layer(features)
		
		priority = self.priority_scorer(features)
		department = self.department_classifier(features)
		return priority, department


model = CustomerTicketModel(num_departments=4)
priority, department = model(
	{'title': title_data, 'text_body': text_body_data, 'tags': tags_data}
)
```

## Обучение модели

После выбора функции потерь, оптимизатора и метрик можно использовать встроенные методы compile() и fit(), чтобы начать обучение модели. При желании можно также реализовать собственные циклы обучения.

### Compile

Метод **compile()** настраивает процесс обучения. Он принимает аргументы с оптимизатором, функцией потерь и метриками (в виде списка).

**Пример вызова compile():**

```Python
model = keras.Sequential([keras.layers.Dense(1)])
model.compile(
	optimizer='rmsprop',
	loss='mean_squared_error',
	metrics=['accuracy']
)
```

В общем случае нет необходимости прописывать функции потерь, метрики или оптимизаторы с нуля, поскольку Keras предлагает широкий спектр встроенных опций, среди которых наверняка найдется то, что нужно для конкретной ситуации:

- **Оптимизаторы:** 

	- SGD (с импульсом или без). 
	
	- RMSprop.
	
	- Adam.
	
	- Adagrad и др.

- **Функции потерь:**

	- CategoricalCrossentropy.
	
	- SparseCategoricalCrossentropy.
	
	- BinaryCrossentropy.
	
	- MeanSquaredError.
	
	- KLDivergence.
	
	- CosineSimilarity и др.

- **Метрики:** 
	
	- CategoricalAccuracy.
	
	- SparseCategoricalAccuracy.
	
	- BinaryAccuracy. 
	
	- AUC.
	
	- Precision.
	
	- Recall и др.

### Fit

За вызовом compile() следует вызов **fit()**. Метод **fit()** реализует собственно цикл обучения. 

**Основные аргументы метода fit():**

- Данные для обучения (исходные данные и целевые значения). Обычно передаются в виде [[Ndarray|массивов NumPy]] или объекта Dataset из библиотеки TensorFlow.

- Количество эпох обучения - сколько раз должен повториться цикл обучения на переданных данных. 

- Размер пакета для использования в каждой эпохе обучения методом градиентного спуска - количество обучающих образцов, учитываемых при вычислении градиентов в одном шаге обновления весов.

**Пример вызова fit():**

```Python
history = model.fit(inputs, targets, epochs=5, batch_size=128)
```

Вызов **fit()** возвращает объект History с полем history — словарем, ключами которого служат имена метрик или строки (такие как "loss"), а значениями — списки значений соответствующих метрик, полученных в разные эпохи.

Для оценки качества модели — того, как она справляется со своей задачей на новых данных, — обычно принято выделять некоторую часть исходных данных в отдельную проверочную выборку: данные из этой выборки не участвуют в обучении модели, но используются для вычисления величины потерь и метрик. Проверочную выборку можно передать методу **fit()** в аргументе validation_data. По аналогии с обучающими данными проверочные данные могут передаваться в форме [[Ndarray|массива NumPy]] или объекта Dataset из библиотеки TensorFlow.

**Пример использования аргумента validation_data:**

```Python
model = keras.Sequential([keras.layers.Dense(1)])

model.compile(
	optimizer=keras.optimizers.RMSprop(learning_rate=0.1),
	loss=keras.losses.MeanSquaredError(),
	metrics=[keras.metrics.BinaryAccuracy()]
)

indices_permutation = np.random.permutation(len(inputs))
shuffled_inputs = inputs[indices_permutation]
shuffled_targets = targets[indices_permutation]

num_validation_samples = int(0.3 * len(inputs))

val_inputs = shuffled_inputs[:num_validation_samples]
val_targets = shuffled_targets[:num_validation_samples]

training_inputs = shuffled_inputs[num_validation_samples:]
training_targets = shuffled_targets[num_validation_samples:]

model.fit(
	training_inputs,
	training_targets,
	epochs=5,
	batch_size=16,
	validation_data=(val_inputs, val_targets)
)
```

**Потери на проверочных данных и метрики можно вычислить после завершения обучения вызовом метода evaluate():** 

```Python
loss_and_metrics = model.evaluate(val_inputs, val_targets, batch_size=128)
```

Метод `evaluate()` выполнит итерации по пакетам (размером batch_size) с переданными данными и вернет список скаляров, первый из которых — величина потерь на проверочных данных, а последующие — метрики. Если модель не имеет метрик, то возвращено будет только одно значение — величина потерь на проверочных данных (а не список).

### Использование собственных метрик 

Метрики являются ключом к оценке качества модели — в частности, они позволяют измерить разницу качества модели на обучающих и контрольных данных. Метрики, обычно используемые для классификации и регрессии, уже включены в стандартный модуль keras.metrics, и в большинстве случаев вы будете брать именно их. Но иногда, особенно при решении необычных задач, вам может понадобиться умение писать свои метрики.

Метрики в [[TensorFlow#^8b88d6|Keras]] являются подклассом класса keras.metrics.Metric. Подобно слоям, метрики имеют внутреннее состояние, хранящееся в [[Тензоры в TensorFlow#^75fb9d|переменных TensorFlow]]. Но, в отличие от слоев, эти переменные не обновляются на этапе обратного распространения, поэтому вам придется написать свою логику их обновления в методе `update_state()`.

**Пример кастомной метрики:**

```Python
import tensorflow as tf


class RootMeanSquaredError(tf.keras.metrics.Metric):
	def __init__(self, name='rmse', **kwargs):
		super().__init__(name=name, **kwargs)
		self.mse_sum = self.add_weight(
			name='mse_sum', 
			initializer='zeros'
		) 
		self.total_samples = self.add_weight(
			name='total_samples', 
			initializer='zeros', dtype='int32'
		)

	def update_state(self, y_true, y_pred, sample_weight=None):
		y_true = tf.one_hot(y_true, depth=tf.shape(y_pred)[1])\
		mse = tf.reduce_sum(tf.square(y_true - y_pred))
		self.mse_sum.assign_add(mse)
		num_samples = tf.shape(y_pred)[0]
		self.total_samples.assign_add(num_samples)

	# Для получения текущего значения метрики
	def result(self): 
		return tf.sqrt(self.mse_sum / tf.cast(self.total_samples, tf.float32))

	# Для сброса состояния
	def reset_state(self):
		self.mse_sum.assign(0.)
		self.total_samples.assign(0)

```
\
Использование такой метрики:

```Python
model = get_mnist_model()

model.compile(
	optimizer='rmsprop',
	loss='sparse_categorical_crossentropy',
	metrics=['accuracy', RootMeanSquaredError()]
)

model.fit(
	train_images,
	train_labels,
	epochs=3,
	validation_data=(val_images, val_labels)
)
test_metrics = model.evaluate(test_images, test_labels)
```

## Использование модели после обучения

После обучения модель можно использовать для вычисления прогнозов на основе новых данных. Этот этап называется выводом. Простейший способ получить прогноз — вызвать модель.\

**Вызов модели:**

```Python
predictions = model(new_inputs)
```

Однако это подразумевает обработку сразу всех входных данных в new_inputs, что может оказаться невыполнимым, если, например, объем данных для прогнозирования слишком большой и для его обработки требуется больше памяти, чем имеется у вашего графического процессора. Лучший способ получить вывод — использовать метод `predict()`. Он выполнит обход данных, разбив их на небольшие пакеты, и вернет массив NumPy с прогнозами. В отличие от вызова, он также может обрабатывать объекты Dataset.

**Предсказание при помощи predict():**

```Python
predictions = model.predict(new_inputs, batch_size=128)
```

## Сохранение и загрузка модели

Модель всегда можно сохранить вручную в виде файла после обучения.

**Сохранение модели:**

```Python
model.save('file_path')
```

Любую сохраненную модель можно загрузить из файла.

**Загрузка  модели:**

```Python
from tensorflow import keras

model = keras.models.load_model('model.keras')
```