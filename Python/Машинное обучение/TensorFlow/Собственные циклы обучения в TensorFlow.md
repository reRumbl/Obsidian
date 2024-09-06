Рабочий процесс на основе метода `fit()` обеспечивает хороший баланс между простотой и гибкостью. Именно этот подход вы будете использовать чаще всего. Однако он не предназначен для поддержки нужд исследователей глубокого обучения, даже несмотря на возможность настройки метрик, функций потерь и обратных вызовов.

В конце концов, подход с использованием метода `fit()` ориентирован исключительно на обучение с учителем, когда заранее известны цели (также называемые метками или аннотациями), связанные с входными данными, а потери вычисляются как функция этих целей и прогнозов модели. Однако не все формы машинного обучения попадают в эту категорию. В некоторых случаях нет явных целей — например, в генеративном обучении, в самоконтролируемом обучении (когда цели извлекаются из входных данных) и в обучении с подкреплением (когда обучение подкрепляется «вознаграждениями», что очень напоминает дрессировку собаки). Даже если вы регулярно занимаетесь обучением с учителем, вам, как исследователю, может понадобиться добавить несколько новых опций, а для этого нужна гибкость на низком уровне.

**Порядок проведения типичного цикла обучения по основным этапам:**

1. Выполнить прямой проход (вычислить выходы модели) внутри [[GradientTape|GradientTape]], чтобы получить величину потерь для текущего пакета данных.

2. Получить градиенты потерь с учетом весов модели.

3. Скорректировать веса модели, чтобы уменьшить величину потерь на текущем пакете данных.

Эти шаги повторяются для выбранного количества пакетов. Фактически именно так и действует метод `fit()`.

Некоторые слои [[TensorFlow#^8b88d6|Keras]] (такие как Dropout) во время обучения и во время прогнозирования ведут себя по-разному. Метод `call()` таких слоев принимает логический аргумент training. Вызов `dropout(inputs, training=True)` приведет к сбросу некоторых активаций, а вызов `dropout(inputs, training=False)` — нет. Кроме того, метод `call()` функциональных и последовательных моделей тоже поддерживает аргумент training. Важно не забывать передавать `training=True` при выполнении прямого прохода модели [[TensorFlow#^8b88d6|Keras]]! То есть прямой проход фактически должен выполняться инструкцией `predictions = model(inputs, training=True)`.

Также обратите внимание, что для получения градиентов весов модели следует использовать не `tape.gradients(loss, model.weights)`, а `tape.gradients(loss, model.trainable_weights)`. В действительности слои и модели обладают двумя видами весов, такими как:

- Обучаемые веса — предназначены для обновления на этапе обратного распространения ошибки, чтобы минимизировать потери модели, такие как ядро и систематическая ошибка слоя Dense.

- Необучаемые веса — предназначены для обновления на этапе прямого прохода слоями, которым они принадлежат. Например, если вы решите добавить в свой слой счетчик пакетов, обработанных к данному моменту, то эта информация будет храниться в необучаемом весе и после обработки каждого пакета ваш слой будет увеличивать счетчик на единицу.

Из встроенных слоев [[TensorFlow#^8b88d6|Keras]] необучаемые веса имеет только слой BatchNormalization. Необучаемые веса нужны слою BatchNormalization для запоминания среднего и стандартного отклонения обрабатываемых данных, чтобы потом динамически выполнить нормализацию признаков.

**Этап обучения с учителем в конечном итоге будет выглядеть следующим образом:**

```Python
def train_step(inputs, targets):
	with tf.GradientTape() as tape:
		predictions = model(inputs, training=True)
		loss = loss_function(targets, predictions)
	gradients = tape.gradients(loss, model.trainable_weights)
	optimizer.apply_gradients(zip(model.trainable_weights, gradients))
```

В низкоуровневом цикле обучения часто возникает необходимость использовать метрики [[TensorFlow#^8b88d6|Keras]] (и стандартные, и нестандартные). Просто вызовите `update_state(y_true, y_pred)` для каждого пакета целей и прогнозов и `result()` для получения текущего значения метрики:

```Python
metric = keras.metrics.SparseCategoricalAccuracy()
targets = [0, 1, 2]
predictions = [[1, 0, 0], [0, 1, 0], [0, 0, 1]]
metric.update_state(targets, predictions) 
current_result = metric.result() 
print(f'Result: {current_result:.2f}')
```

Вам также может потребоваться отслеживать среднее значение скаляра, например величины потери модели. Это можно сделать с помощью метрики keras.metrics.Mean: 

```Python
values = [0, 1, 2, 3, 4]
mean_tracker = keras.metrics.Mean()
for value in values:
	mean_tracker.update_state(value)
	print(f'Mean of values: {mean_tracker.result():.2f}') 
```

Не забудьте вызвать metric.reset_state(), когда понадобится сбросить текущий результат (в начале эпохи обучения или в начале этапа оценки).

**Шаговая функция обучения:**

```Python
model = get_mnist_model()

loss_function = keras.losses.SparseCategoricalCrossentropy() 
optimizer = keras.optimizers.RMSprop() 
metrics = [keras.metrics.SparseCategoricalAccuracy()] 
loss_tracking_metric = keras.metrics.Mean() 


def train_step(inputs, targets): 
	with tf.GradientTape() as tape: 
		predictions = model(inputs, training=True)
		loss = loss_function(targets, predictions)
	gradients = tape.gradient(loss, model.trainable_weights) 
	optimizer.apply_gradients(zip(gradients, model.trainable_weights)) 
	
	logs = {} 
	for metric in metrics: 
		metric.update_state(targets, predictions)
		logs[metric.name] = metric.result() 
		
	loss_tracking_metric.update_state(loss) 
	logs['loss'] = loss_tracking_metric.result()
	return logs
```

Важно не забыть сбросить состояние метрик в начале каждой эпохи и перед началом этапа оценки.

**Сброс метрик:**

```Python
def reset_metrics(): 
	for metric in metrics: 
		metric.reset_state() 
	loss_tracking_metric.reset_state()
```

Теперь можно закончить реализацию цикла обучения. Обратите внимание, что здесь используется объект tf.data.Dataset, превращающий массив NumPy с данными в итератор, который выполняет итерации по данным пакетами размером 32.

**Цикл обучения:**

```Python
training_dataset = tf.data.Dataset.from_tensor_slices((train_images, train_labels))
training_dataset = training_dataset.batch(32)
epochs = 3 

for epoch in range(epochs): 
	reset_metrics() 
	for inputs_batch, targets_batch in training_dataset: 
		logs = train_step(inputs_batch, targets_batch)
	print(f'Results at the end of epoch {epoch}') 
	for key, value in logs.items():
		print(f'...{key}: {value:.4f}')
```

Ниже приводится цикл оценки: простой цикл for, многократно вызывающий функцию `test_step()`, которая обрабатывает один пакет данных. Функция `test_ step()` — лишь подмножество логики `train_step()`. В ней отсутствует код, обновляющий веса модели, то есть все, что связано с GradientTape и оптимизатором.

```Python
def test_step(inputs, targets): 
	predictions = model(inputs, training=False) 
	loss = loss_fn(targets, predictions) 
	
	logs = {} 
	for metric in metrics: 
		metric.update_state(targets, predictions) 
		logs['val_' + metric.name] = metric.result() 
		
	loss_tracking_metric.update_state(loss)
	logs['val_loss'] = loss_tracking_metric.result() 
	return logs 


val_dataset = tf.data.Dataset.from_tensor_slices((val_images, val_labels)) 
val_dataset = val_dataset.batch(32) 
reset_metrics() 
for inputs_batch, targets_batch in val_dataset: 
	logs = test_step(inputs_batch, targets_batch) 
print('Evaluation results:')
for key, value in logs.items():
	print(f'...{key}: {value:.4f}')
```

Закончив отладку, код можно ускорить, добавив декоратор `@tf.function` перед функциями, реализующими шаг обучения и шаг оценки, или любыми другими функциями, для которых важна высокая производительность.

**Реализация своего шага обучения для использования с `fit()`:**

```Python
loss_function = keras.losses.SparseCategoricalCrossentropy()
loss_tracker = keras.metrics.Mean(name='loss')


class CustomModel(keras.Model): 
	def train_step(self, data): 
		inputs, targets = data
		with tf.GradientTape() as tape: 
			predictions = self(inputs, training=True) 
			loss = loss_fn(targets, predictions)
		 gradients = tape.gradient(loss, model.trainable_weights) 
		 optimizer.apply_gradients(zip(gradients, model.trainable_weights)) 
		 
		 loss_tracker.update_state(loss) 
		 return {'loss': loss_tracker.result()} 
		 
	@property 
	def metrics(self): 
		return [loss_tracker]


# Обучение модели
inputs = keras.Input(shape=(28 * 28,)) 
features = layers.Dense(512, activation=;'relu')(inputs)
features = layers.Dropout(0.5)(features) 
outputs = layers.Dense(10, activation='softmax')(features) 
model = CustomModel(inputs, outputs)

model.compile(optimizer=keras.optimizers.RMSprop()) 
model.fit(train_images, train_labels, epochs=3)
```

*Примечание: при переопределении метода train_step не нужно использовать декоратор `@tf.function` — фреймворк сделает это автоматически.*