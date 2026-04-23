Работа с файлами в [[FastAPI|FastAPI]] осуществляется через специальные [[Классы|классы]], связанные с загрузкой и обработкой файлов.

## Загрузка файла на сервер

Чтобы загрузить файл на сервер используется [[Классы|класс]] `UploadFile`. Основные атрибуты данного [[Классы|класса]]:

- `file` - Сам файл.

- `filename` - Имя файла.

- `size` - Размер файла (в байтах).

**Пример [[Endpoint, Параметры URL в FastAPI|endpoint]] для загрузки одного файла:**

```Python
from fastapi import UploadFile

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

## Скачивание файлов с сервера

Чтобы скачать файл с сервера используются [[Классы|класс]] `FileResnonse` (`StreamingResponse` в случае транслирования файла кусками и/или из другого сервиса, например [[S3 Хранилище|S3 хранилища]]).

**Пример endpoint для скачивания файла, который хранится локально на сервере:**

```Python
from fastapi.responses import FileResponse


@app.get('/files/{filename}')
async def get_file(filename: str):
	return FileResponse(filename)
```

**Пример [[Endpoint, Параметры URL в FastAPI|endpoint]] для скачивания файла, который хранится на стороннем ресурсе:**

Для отправки файла кусками при помощи `StreamingResponse` требуется генератор:

```Python
def get_file_chunk(filename: str):
	with open(filename, 'rb') as file:
		while chunk := file.read(1024 * 1024):  # Размер чанка - 1 Мб
			yield chunk
```

Далее сам endpoint использует написанный выше генератор, например для отправки видео файла формата mp4 кусками:

```Python
from fastapi.responses import StreamingResponse


@app.get('/files/streaming/video/{filename}')
async def get_video_chunk(filename: str):
	return StreamingResponse(get_file_chunk(filename), media_type='video/mp4')
```