**Роутер** - это инструмент, который помогает организовывать и группировать маршруты (пути) веб-приложения. Он позволяет собрать функции, которые отвечают за разные URL-адреса, в одно место и добавить их в основное приложение.

**Пример создания роутера:**

```Python
from fastapi import APIRouter, Depends
from sqlalchemy import AsyncSession

from src import models, schemas, crud
from src.database import get_db

track_router = APIRouter(
	prefix='/track',
	tags=['Track']
)


router.get('/{track_id}', response_model=schemas.Track)
async def get_track(track_id, db: AsyncSession = Depends(get_db)):
	return crud.get_track(db, track_id)
```

**Подключение роутера к основному приложению:**

```Python
from fastapi import FastAPI

from src.routers import track_router

app = FastAPI()

app.include_router(track_router)
```