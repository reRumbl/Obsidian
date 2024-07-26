Обработка ошибок в FastAPI происходит при помощи привычных [[Исключения|конструкций исключений]]. При возвращении ошибки желательно придерживаться одной структуры, н

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

router.get('/{track_id}', response_model=schemas.Track)
async def get_track(track_id, db: AsyncSession = Depends(get_db)):
	try:
		return crud.get_track(db, track_id)
	except Exception as e:
		return {
			'status': 'error',
			'data': None,
			'details': None
		}
```