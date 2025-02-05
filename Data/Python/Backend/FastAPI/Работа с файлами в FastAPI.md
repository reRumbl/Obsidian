Работа с файлами в [[FastAPI|FastAPI]] осуществляется через специальные [[Классы|классы]] `File` и `UploadFile`.

```Python
from fastapi import FastAPI, File, UploadFile
```

## Загрузка файла на сервер

Чтобы загрузить файл на сервер используется [[Классы|класс]] `UploadFile`. Он содержит такие атрибуты, как:

- `file` - Сам файл.
-  (.)

**Пример endpoint для загрузки файла:**

```Python
app = FastAPI()

@app.post('/files')
async def upload_file(uploaded_file: UploadFile):
	file = uploaded_file.file
	filename = 
```