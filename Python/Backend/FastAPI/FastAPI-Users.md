**FastAPI Users** - это мощная библиотека, разработанная для создания аутентификации в [[FastAPI|FastAPI]].

![[FastAPI-Users.png]]

**Установка через cmd или terminal:**

```Python
pip install fastapi-users[sqlalchemy]  # С поддержкой SQLAlchemy
pip install fastapi-users[beanie]  # С поддержкой Beanie
```

**Подключение в проект:**

```Python
import fastapi_users
```

## Подключение к БД

Для [[Аутентификация в FastAPI|аутентификации]] через **FastAPI-Users** требуется настроить подключение к БД. Для этого следует продублировать модель пользователя в новом файле, [[Наследование|наследуя]] ее от специального [[Классы|класса]].

**Подключение к БД (SQLAlchemy):**

```Python
from typing import AsyncGenerator  
  
from fastapi import Depends  
from fastapi_users.db import SQLAlchemyBaseUserTable, SQLAlchemyUserDatabase  
from sqlalchemy.ext.asyncio import AsyncSession, async_sessionmaker, create_async_engine  
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column, relationship  
from src.config import settings  
from src.models import int_pk, unique_str, optional_str, created_at, updated_at  
  
DATABASE_URL = settings.database_url_asyncpg  
  
  
class Base(DeclarativeBase):  
    pass  
  
  
class User(SQLAlchemyBaseUserTable[int], Base):  
    id: Mapped[int_pk]  
    username: Mapped[unique_str]  
    description: Mapped[optional_str]  
    hashed_password: Mapped[str]  
    email: Mapped[unique_str]  
  
    is_active: Mapped[bool] = mapped_column(default=True, nullable=False)  
    is_admin: Mapped[bool] = mapped_column(default=False, nullable=False)  
    is_verified: Mapped[bool] = mapped_column(default=False, nullable=False)  
  
    tracks = relationship('Track', secondary='m2m_users_tracks', back_populates='users')  
  
    created_at: Mapped[created_at]  
    updated_at: Mapped[updated_at]  
  
  
engine = create_async_engine(DATABASE_URL)  
async_session_maker = async_sessionmaker(engine, expire_on_commit=False)  
  
  
async def get_async_session() -> AsyncGenerator[AsyncSession, None]:  
    async with async_session_maker() as session:  
        yield session  
  
  
async def get_user_db(session: AsyncSession = Depends(get_async_session)):  
    yield SQLAlchemyUserDatabase(session, User)
```
