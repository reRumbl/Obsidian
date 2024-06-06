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

**Прохождение по всем файлам и директориям в указанной директории:**

```Python
for root, dirs, files in walk(directory):
	# Do something
```

**Удаление файлов и директорий:**

*При помощи remove (только файлы):*

```Python
file = 'image1.jpg'
location = 'R:/Pycharm/New Project/data/images/'
path = os.path.join(location, file) 
os.remove(path)
```

*При помощи rmdir (только пустые папки):*

```Python
directory = 'csv'
parent = 'R:/Pycharm/New Project/data'
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
os.rename('R:/file.txt', 'renamed.txt')
```

**Проверка на наличие пути к файлу:**

```Python
if os.path.exists('file_name'):
	print('File exists')
```

**Проверка на то, является ли объект фалом или папкой:**

*Проверка на папку:*

```Python
if os.path.isdir('R:/Pycharm'):
	print('This is a directory')
```

*Проверка на файл:*

```Python
if os.path.isfile('R:/file/txt'):
	print('This is a file')
```

**Получение размера файла:**

```Python
size = os.path.getsize('filename')
```