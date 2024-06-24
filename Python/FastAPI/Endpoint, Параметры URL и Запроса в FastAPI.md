**Endpoint** - это альтернативное название пути в веб-приложении. В [[FastAPI|FastAPI]] можно легко создавать **endpoint**, добавляя декораторы к соответствующим функциям обработчикам.

**Пример создания endpoint:**

```Python
from fastapi import FastAPI

app = Fast


@app.get('/')
def read_root():
    return {'message': 'Hello, World!'}
```