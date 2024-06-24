Для валидации данных в [[FastAPI|FastAPI]] обычно используется библиотека [[Pydantic|Pydantic]].

**Пример валидации данных в приложении при помощи Pydantic:**

```Python
import uvicorn
from fastapi import FastAPI
from pydantic import BaseModel, Field, PositiveFloat

app = FastAPI(title='Item Validation App')


@app.get('/')
def read_root():
    return {'message': 'Hello, World!'}


@app.get("/items/{item_id}")
def get_item_id(item_id: int):
    return {'item_id': item_id, 'message': f'Item id is {item_id}'}


class Item(BaseModel):
    name: str
    description: str | None = None
    price: PositiveFloat


id_list = []


@app.post('/items/')
def create_item(item: Item):
    item_id = len(id_list) + 1
    new_item = item.dict()
    new_item['id'] = item_id
    id_list.append(new_item['id'])
    return new_item

if __name__ == '__main__':
    uvicorn.run(app, host='127.0.0.1', port=8000)

```