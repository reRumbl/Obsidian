Работа с файлами в [[FastAPI|FastAPI]] осуществляется через специальные [[Классы|классы]] `File` и `UploadFile`.

```Python
from fastapi import FastAPI, File, UploadFile
```

## Загрузка файла на сервер

Чтобы загрузить файл на сервер используется [[Классы|класс]] `UploadFile`. Основные атрибуты данного [[Классы|класса]]:

- `file` - Сам файл.

- `filename` - Имя файла.

- `size` - Размер файла (в байтах).

**Пример endpoint для загрузки одного файла:**

```Python
app = FastAPI()

@app.post('/files')
async def upload_file(uploaded_file: UploadFile):
	file = uploaded_file.file
	filename = uploaded_file.filename  # Имя файла может быть любое
	
	with open(filename, 'wb', ) as f:
		f.write(file.read())
```

**Пример endpoint для загрузки нескольких файлов:**

```Python
@app.post('/multiple_files')
async def upload_multiple_files(uploaded_files: list[UploadFile]):
	for uploaded_file in uploaded_files:
		file = uploaded_file.file
		filename = uploaded_file.filename  # Имя файла может быть любое
		
		with open(filename, 'wb', ) as f:
			f.write(file.read())
```

