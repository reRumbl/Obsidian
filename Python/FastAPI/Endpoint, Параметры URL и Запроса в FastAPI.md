**Endpoint** - это альтернативное название пути в веб-приложении. В [[FastAPI|FastAPI]] можно легко создавать **endpoint**, добавляя [[Декораторы|декораторы]] к соответствующим функциям обработчикам.

**Пример создания endpoint:**

```Python
from fastapi import FastAPI

app = FastAPI()


@app.get('/')
def get_hello():
    return {'message': 'Hello, World!'}
```

Для передачи параметров через URL нужно указать название этих параметров в фигурных скобках при создании **endpoint**. А добавить этот параметр в качестве аргумента функции, к которой прилагается соответствующий [[Декораторы|декоратор]].

**Пример передачи параметров через URL:**

```Python
from fastapi import FastAPI

app = FastAPI()


@app.get("/items/{item_id}")
def get_item_id(item_id: int):
    return {'item_id': item_id,
            'message': f'Item id is {item_id}'}
```

Пример