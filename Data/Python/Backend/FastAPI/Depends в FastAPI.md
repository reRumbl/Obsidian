**Depends** - это специальный [[Классы|класс]] в [[FastAPI|FastAPI]], который позволяет добавлять зависимости к функциям.

**Пример подключения зависимости базы данных:**

```Python
from typing import Annotated
from fastapi import FastAPI, Depends
from app.database.session import get_db

app = FastAPI()


@app.get('/items')
async def get_items(db: AsyncSession = Depends(get_db)):
    pass


# Or
SessionDep = Annotated[AsyncSession, Depends(get_db)]


@app.get('/items')
async def get_items(db: SessionDep):
    pass
```

**Пример зависимости для пагинации страниц:**

```Python
from typing import Annotated
from fastapi import FastAPI, Depends
from pydantic import BaseModel, Field

app = FastAPI()

  
class PaginationParams(BaseModel):
    limit: int = Field(10, ge=0, le=100)
    offset: int = Field(0, ge=0)


PaginationDep = Annotated[PaginationParams, Depends(PaginationParams)]

  
@app.get('/items')
async def get_items(pagination: PaginationDep):
    pass
```