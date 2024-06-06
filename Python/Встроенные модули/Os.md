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

**Создание директории:**

*При помощи mkdir (создается одна папка):*

```Python
directory = "New Project"
parent_dir = "R:/Pycharm/"
path = os.path.join(parent_dir, directory)

os.mkdir(path)
```

*При помощи makedirs (папки создаются рекурсивно, в случае отсутствия):*

```Python
directory = "images"
parent_dir = "R:/Pycharm/New Project/data"
path = os.path.join(parent_dir, directory)

os.makedirs(path)
```

**Получение списка файлов в директории:**

```Python
path = "/"
dir_list = os.listdir(path)
```