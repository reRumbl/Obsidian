Проектирование RestAPI включает в себя обработку ошибок и четкое структурирование.

## Обработка ошибок

Обработка ошибок в FastAPI происходит при помощи привычных [[Исключения|конструкций исключений]].

**Обработка ошибок в endpoint:**

```Python
from fastapi import APIRouter, Depends
from sqlalchemy import AsyncSession

from src import models, schemas, crud
from src.database import get_db

track_router = APIRouter(
	prefix='/track',
	tags=['Track']
)


router.get('/{track_id}')
async def get_track(track_id, db: AsyncSession = Depends(get_db)):
	try:
		return {
			'status': 'error',
			'data': crud.get_track(db, track_id),
			'details': None
		}
	except Exception as e:
		return {
			'status': 'error',
			'data': None,
			'details': None
		}
```

Пользователю можно возвращать детали ошибки и ее код, при помощи HTTPException. 

Диапазоны кодов ответов HTTP:

- 1xx - Информационные

**Возврат ошибки пользователю:**

```Python
from fastapi import APIRouter, Depends, HTTPException
from sqlalchemy import AsyncSession

from src import models, schemas, crud
from src.database import get_db

track_router = APIRouter(
	prefix='/track',
	tags=['Track']
)


router.get('/{track_id}')
async def get_track(track_id, db: AsyncSession = Depends(get_db)):
	try:
		return {
			'status': 'error',
			'data': crud.get_track(db, track_id),
			'details': None
		}
	except Exception as e:
		raise HTTPException(status_code=400, detail={
			'status': 'error',
			'data': None,
			'details': None
		}
```
## Структура

При возвращении JSON желательно придерживаться одной структуры, будь то ошибка или успешное выполнение операции. Такой подходит упрощает работу с API как разработчикам, так и обычным пользователям.

**Пример структуры JSON:**

```JSON
{
	'status': 'error',
	'data': None,
	'details': None
}
```