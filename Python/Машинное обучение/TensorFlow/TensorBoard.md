[TensorBoard](https:/www.tensorflow.org/tensorboard) — браузерное приложение, которое можно запускать локально. Это лучший способ наблюдения за происходящим внутри модели во время обучения. [TensorBoard](https:/www.tensorflow.org/tensorboard) позволяет:

- Визуально контролировать метрики в процессе обучения. 

- Отображать архитектуру модели.

- Выводить гистограммы активаций и градиентов.

- Исследовать векторные представления в трехмерной системе координат.

![[TensorBoard.png]]

Самый простой способ использовать [TensorBoard](https:/www.tensorflow.org/tensorboard) с [[Модели в TensorFlow|моделью]] [[TensorFlow#^8b88d6|Keras]] и методом `fit()` — определить [[Обратные вызовы в TensorFlow|обратный вызов]] `keras.callbacks.TensorBoard`. В простейшем случае достаточно указать, куда должна записываться информация этим [[Обратные вызовы в TensorFlow|обратным вызовом]], и все.

**Пример использования TensorBoard:**

```Python
model = get_mnist_model()
model.compile(
	optimizer='rmsprop',
	loss='sparse_categorical_crossentropy',
	metrics=['accuracy']
)
tensorboard = keras.callbacks.TensorBoard(log_dir='/full_path_to_log_dir')
model.fit(
	train_images,
	train_labels,
	epochs=10,
	validation_data=(val_images, val_labels),
	callbacks=[tensorboard]
)
```

С началом обучения модель будет записывать информацию в указанное местоположение.  Обратите внимание, что выполняемый файл tensorboard уже должен быть доступен, если библиотека TensorFlow устанавливалась с помощью pip. Если нет, можно установить TensorBoard вручную командой pip install tensorboard.

**Если обучение выполняется на локальном компьютере, то вы можете запустить локальный сервер TensorBoard следующей командой:**

```Shell
tensorboard --logdir /full_path_to_log_dir
```

*Примечание: Данная команда выведет URL, который затем можно ввести в адресную строку браузера, чтобы получить доступ к интерфейсу TensorBoard.*

**Если обучение производится в блокноте Colab, то можно запустить встроенный экземпляр TensorBoard в блокноте, выполнив следующую команду:**

```Shell
%load_ext tensorboard
%tensorboard --logdir /full_path_to_your_log_dir
```

**В интерфейсе TensorBoard можно наблюдать в режиме реального времени, как протекает процесс обучения модели:**

![[Вид TensorBoard.png]]