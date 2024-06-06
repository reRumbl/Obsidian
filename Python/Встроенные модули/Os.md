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
directory = 'New Project'
parent_dir = 'R:/Pycharm/'
path = os.path.join(parent_dir, directory)

os.mkdir(path)
```

*При помощи makedirs (папки создаются рекурсивно, в случае отсутствия):*

```Python
directory = 'images'
parent_dir = 'R:/Pycharm/New Project/data'
path = os.path.join(parent_dir, directory)

os.makedirs(path)
```

**Получение списка файлов в директории:**

```Python
path = 'R:/Pycharm/New Project'
dir_list = os.listdir(path)
```

**Удаление файлов и директорий:**

*При помощи remove (только файлы):*

```Python
file = 'image1.jpg'
location = "D:/Pycharm/New Project/data/images/"
path = os.path.join(location, file) 
os.remove(path)
```

*При помощи rmdir (только пустые папки):*

```Python
directory = "csv"
parent = "D:/Pycharm/New Project/data
path = os.path.join(parent, directory) 
os.rmdir(path)
```

**Открытие и закрытие файлов:**

*Открытие:*

```Python
file = os.popen('D:/file.txt')
```

*Закрытие:*

```Python
os.close(file)
```

**Переименование файла:**

```Python
os.rename('D:/file.txt', 'renamed.txt')
```

**Проверка на наличие пути к файлу:**

```Python
result = os.path.exists("file_name")
```

**Получение размера файла:**

```Python
size = os.path.getsize("filename")
```