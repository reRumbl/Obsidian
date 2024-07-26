**Роутер** - это инструмент, который помогает организовывать и группировать маршруты (пути) веб-приложения. Он позволяет собрать функции, которые отвечают за разные URL-адреса, в одно место и добавить их в основное приложение.

**Пример создания роутера:**

```Python
from fastapi import APIRouter

from src import models, schemas, crud, database

router = APIRouter(
	prefix='/track',
	tags=['Track']
)

router.get('/{track_id}', response_model=schemas.Track)
async def get_track(track_id):
	return crud.get_track(database.get_db(), track_id)
```

Подключение роутера к основному приложению:

```Pyt
```