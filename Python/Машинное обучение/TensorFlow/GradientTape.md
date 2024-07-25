Роль интерфейса для управления мощными возможностями автоматического дифференцирования в [[Tensorflow|TensorFlow]] играет **GradientTape**. Это объект на [[Python|Python]], который «записывает» выполняемые тензорные операции в форме графа вычислений (иногда называемого tape — лентой). Этот граф затем можно использовать для получения градиента любого результата относительно любой переменной или набора переменных (экземпляров класса tf.Variable). 

**GradientTape** — мощный объект, способный даже вычислять градиенты второго порядка, то есть градиенты градиентов. Например, градиент положения объекта относительно времени — это скорость объекта, а градиент второго порядка — его ускорение

Класс tf.Variable представляет особый вид тензора, предназначенный для хранения изменяемого состояния: например, веса нейронной сети всегда являются экземплярами tf.Variable.

**Пример использования GradientTape:**

```Python
import tensorflow as tf

x = tf.Variable(0.)  # Экземпляр tf.Variable со скалярным значением 0
with tf.GradientTape() as tape:  # Открытие контекста GradientTape
	y = 2 * x + 3  # Применение тензорных операций к переменной внутри контекста
grad_of_y_wrt_x = tape.gradient(y, x)  # Использование tape для излвечения градиента
```

**GradientTape работает с тензорными операциями:**

```Python
x = tf.Variable(tf.random.uniform((2, 2)))
with tf.GradientTape() as tape:
	y = 2 * x + 3
grad_of_y_wrt_x = tape.gradient(y, x)
```

**И со списками переменных:**

```Python
W = tf.Variable(tf.random.uniform((2, 2)))
b = tf.Variable(tf.zeros((2,)))
x = tf.random.uniform((2, 2))
with tf.GradientTape() as tape:
	y = tf.matmul(x, W) + b
grad_of_y_wrt_W_and_b = tape.gradient(y, [W, b])
```