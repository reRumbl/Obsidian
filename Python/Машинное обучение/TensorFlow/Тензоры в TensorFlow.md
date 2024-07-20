В любых операциях, выполняемых с помощью [[Tensorflow|TensorFlow]], участвуют тензоры. Тензоры создаются с некоторыми начальными значениями. Например, можно создать тензор с единицами во всех элементах, с нулями или со случайными значениями.

**Создание тензоров с единицами:**

```Python
import tensorflow as tf

x = tf.ones(shape=(2, 1))
print(x)
```

**Создание тензоров с нулями:**

```Python
x = tf.zeros(shape=(2, 1))
print(x)
```

**Создание тензоров со случайными значениями:**

```Python
x = tf.random.normal(shape=(3, 1), mean=0., stddev=1.)
print(x)

x = tf.random.uniform(shape=(3, 1), minval=0., maxval=1.)
print(x)
```

 Существенная разница между массивами [[NumPy|NumPy]] и тензорами [[Tensorflow|Tensorflow]] заключается в том, что тензоры [[Tensorflow|TensorFlow]] не могут изменяться, они подобны константам. Поэтому для управления
изменяемым состоянием в [[Tensorflow|TensorFlow]] применяется [[Классы|класс]] tf.Variable.

**Создание переменной TensorFlow:**

```Python
v = tf.Variable(initial_value=tf.random.normal(shape=(3, 1)))
print(v)
```

## Операции с тензорами

Так же как [[NumPy|NumPy]], [[Tensorflow]] предлагает большую коллекцию тензорных операций для выражения математических формул.

**Примеры тензорных операций:**

*Создание:*

```Python
a = tf.ones((2, 2))
```

*Возведение в квадрат:*

```Python
b = tf.square(a)
```

*Квадратный корень:*

```Python
c = tf.sqrt(b)
```

*Поэлементное сложение:*

```Python
d = b + c
```

*Матричное умножение:*

```Python
e = tf.matmul(a, b)
```

*Поэлементное умножение:*

```Python
e *= d
```