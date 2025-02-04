[[FastAPI|FastAPI]] шаблоны для [[VSCode|Visual Studio Code]].

| Сокращение | Описание                |
| ---------- | ----------------------- |
| hw         | FastAPI hello world     |
| path       | FastAPI GET path        |
| apath      | FastAPI async GET path  |
| pathp      | FastAPI POST path       |
| apathp     | FastAPI async POST path |
| sqldb      | SQLAlchemy Database     |
| getdb      | SessionLocal Dependency |
| stup       | Startup Event           |
| shdn       | Shutdown Event          |

**Пример использования шаблона:**

```Python
# hw -> TAB -> code
from fastapi import FastAPI

app = FastAPI()


@app.get('/')
async def root():
    return {'message': 'Hello World'}
```
