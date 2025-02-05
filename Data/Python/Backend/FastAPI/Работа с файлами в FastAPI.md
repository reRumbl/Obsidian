Работа с файлами в [[FastAPI|FastAPI]] осуществляется через специальные [[Классы|классы]] `File` и `UploadFile`.

```Python
from fastapi import FastAPI, File, UploadFile
```

## Загрузка файла на сервер

Чтобы загрузить файл на сервер используется [[Классы|класс]] `UploadFile`. Основные атрибуты данного [[Классы|класса]]:

- `file` - Сам файл.

- `filename` - Имя файла.

- `size` - Размер файла (в байтах).

**Пример endpoint для загрузки файла:**

```Python
app = FastAPI()

@app.post('/files')
async def upload_file(uploaded_file: UploadFile):
	file = uploaded_file.file
	filename = uploaded_file.filename
	
	with open(filename, 'wb', ) as f:
		f.write(file.read())
```