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

**Конфигурация транспортировки (bearer + jwt):**

```Python
import uuid
from fastapi import Depends
from fastapi_users.authentication import AuthenticationBackend, BearerTransport, JWTStrategy
from app.auth.database import User, get_user_db
from app.config import settings

bearer_transport = BearerTransport(tokenUrl='/api/auth/jwt/login')


def get_jwt_strategy() -> JWTStrategy:
    return JWTStrategy(secret=settings.JWT_SECRET_KEY, lifetime_seconds=3600)


auth_backend = AuthenticationBackend(  
    name='jwt',  
    transport=bearer_transport,
    get_strategy=get_jwt_strategy  
)
```

## Создание UserManager

Далее требуется создать менеджера, который позволит работать с данными пользователей.

**Создание менеджера:**

```Python
import uuid
from fastapi_users import BaseUserManager, UUIDIDMixin
from app.auth.database import User


class UserManager(UUIDIDMixin, BaseUserManager[User, uuid.UUID]):
    reset_password_token_secret = SECRET
    verification_token_secret = SECRET

    async def on_after_register(self, user: User, request: Optional[Request] = None):
        print(f'User {user.id} has registered.')

    async def on_after_forgot_password(
        self, user: User, token: str, request: Optional[Request] = None
    ):
        print(f'User {user.id} has forgot their password. Reset token: {token}')

    async def on_after_request_verify(
        self, user: User, token: str, request: Optional[Request] = None
    ):
        print(f'Verification requested for user {user.id}. Verification token: {token}')


async def get_user_manager(user_db: SQLAlchemyUserDatabase = Depends(get_user_db)):
    yield UserManager(user_db)
```

## Инициализация FastAPI-Users

После всех вышеперечисленных действий требуется инициализировать класс `FastAPIUsers`.

**Инициализация FastAPIUsers:**

```Python
from typing import Annotated
from fastapi import Depends
from fastapi_users import FastAPIUsers
from app.auth.database import User
from app.auth.manager import get_user_manager
from app.auth.transport import auth_backend

fastapi_users = FastAPIUsers[User, uuid.UUID](get_user_manager, [auth_backend])

current_active_user = fastapi_users.current_user(active=True)
CurrentUserDep = Annotated[User, Depends[current_active_user]]
```

## Создание схем

Перед подключением маршрутов нужно создать [[Pydantic|Pydantic]] схемы.

**Создание схем:**

```Python
import uuid
from fastapi_users import schemas


class UserRead(schemas.BaseUser[uuid.UUID]):
    pass


class UserCreate(schemas.BaseUserCreate):
    pass


class UserUpdate(schemas.BaseUserUpdate):
    pass
```

## Подключение маршрутов

В основном файле нужно подключить маршруты из FastAPI-Users

Подключение маршрутов:

```Python
from fastapi import Depends, FastAPI
from app.auth.database import User
from app.auth.schemas import UserCreate, UserRead, UserUpdate
from app.auth.transport import auth_backend
from app.auth.users import fastapi_users

app = FastAPI()

app.include_router(
    fastapi_users.get_auth_router(auth_backend), prefix='/api/auth/jwt', tags=['auth']
)
app.include_router(
    fastapi_users.get_register_router(UserRead, UserCreate),
    prefix='/api/auth',
    tags=['auth'],
)
app.include_router(
    fastapi_users.get_reset_password_router(),
    prefix='/api/auth',
    tags=['auth'],
)
app.include_router(
    fastapi_users.get_verify_router(UserRead),
    prefix='/api/auth',
    tags=['auth'],
)
app.include_router(
    fastapi_users.get_users_router(UserRead, UserUpdate),
    prefix='/api/users',
    tags=['users'],
)
```

## Использование в других маршрутах

Для подключения авторизации в других маршрутах требуется использовать зависимость `current_active_user`.

**Создание защищенного маршрута:**

```Python
from app.auth.users import CurrentUserDep

@app.get('/authenticated-route')
async def authenticated_route(user: CurrentUserDep):
    return {'message': f'Hello {user.email}!'}
```
