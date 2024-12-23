[[Tensorflow|Tensorflow]] предоставляет автоматическое логирование.

## Изменение уровня логирования

По умолчанию все уровни сообщений TensorFlow выводятся в консоль, это можно заметить сразу при импорте библиотеки.

**Сообщения при импорте библиотеки:**

```Shell
2024-07-26 21:40:04.408192: I tensorflow/core/util/port.cc:153] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.  
2024-07-26 21:40:21.752619: I tensorflow/core/util/port.cc:153] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.  
2024-07-26 21:40:31.028982: I tensorflow/core/platform/cpu_feature_guard.cc:210] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.  
To enable the following instructions: AVX2 FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
```

Вывод сообщений можно отключить, предприняв соответствующие меры. Для этого можно редактировать уровень логирования. Установив его значение на 2, TensorFlow перестанет выводить информационные сообщения и предупреждения. Данное значение устанавливается в [[Dotenv|переменном окружении]], при помощи модуля [[Os|os]].

**Установление уровня логирования только на ошибки:**

```Python
import os  
  
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'
```