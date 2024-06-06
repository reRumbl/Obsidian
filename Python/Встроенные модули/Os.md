**Os** - встроенный модуль Python, который позволяет взаимодействовать с ресурсами операционной системы.

![[Os.png]]

**Подключение в проект:**

```Python
import os
```

## Работа с файлами и директориями

**Захват текущей рабочей директории:**

```Python
cwd = os.getcwd() 
print(f'Current working directory: {cwd}')
```

**Изменение текущей рабочей директории:**

```Python
os.chdir('C:/Users/')
```

**Создание директории при помощи mkdir:**

```Python
directory = "New Dir"
parent_dir = "D:/Pycharm projects/"
path = os.path.join(parent_dir, directory)

os.mkdir(path)
```