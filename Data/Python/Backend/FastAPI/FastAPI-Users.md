**FastAPI Users** - это мощная библиотека, разработанная для создания аутентификации в [[FastAPI|FastAPI]].

![[FastAPI-Users.png]]

**Установка через cmd или terminal:**

```Shell
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
from fastapi import Depends
from fastapi_users.db import SQLAlchemyBaseUserTableUUID, SQLAlchemyUserDatabase
from app.database.session import Base, SessionDep


class User(SQLAlchemyBaseUserTableUUID, Base):
    pass


async def get_user_db(session: SessionDep):
    yield SQLAlchemyUserDatabase(session, User)
```

## Конфигурация транспортировки

После подключения к БД следует задать конфигурацию транспортировки в отдельном файле.

**Конфигурация транспортировки (bearer + database):**

```Python
import uuid
from fastapi import Depends
from fastapi_users.authentication import AuthenticationBackend, BearerTransport, JWTStrategy
from app.auth.database import User, get_user_db
from app.config import settings

bearer_transport = BearerTransport(tokenUrl='/api/auth/jwt/login')


def get_database_strategy(
    access_token_db: AccessTokenDatabase[AccessToken] = Depends(get_access_token_db),
) -> DatabaseStrategy:
    return DatabaseStrategy(access_token_db, lifetime_seconds=3600)


auth_backend = AuthenticationBackend(  
    name='database',  
    transport=bearer_transport,
    get_strategy=get_database_strategy  
)
```

## Создание UserManager

Далее требуется создать менеджера, который позволит работать с данными пользователей.

**Создание менеджера:**

```Python
from typing import Optional
from fastapi import Depends, Request  
from fastapi_users import BaseUserManager, IntegerIDMixin  
from .database import User, get_user_db  
from app.config import settings  

SECRET = settings.JWT_KEY  


class UserManager(IntegerIDMixin, BaseUserManager[User, int]):  
    reset_password_token_secret = SECRET  
    verification_token_secret = SECRET 
     
    async def on_after_register(self, user: User, request: Optional[Request] = None):  
        print(f"User {user.id} has registered.")  

    async def on_after_forgot_password(  
        self, user: User, token: str, request: Optional[Request] = None  
    ):  

        print(f"User {user.id} has forgot their password. Reset token: {token}")  

    async def on_after_request_verify(  
        self, user: User, token: str, request: Optional[Request] = None  
    ):  
        print(f"Verification requested for user {user.id}. Verification token: {token}")


async def get_user_manager(user_db=Depends(get_user_db)):  
    yield UserManager(user_db)
```

## Создание схем Pydantic

После всех вышеперечисленных шагов требуется создать схемы Pydantic