**AuthX** - это библиотека на [[Python|Python]] для проектирования авторизации. 

![[AuthX.png]]

**Установка через cmd или terminal:**

```Python
pip install authx
```

**Подключение в проект:**

```Python
import authx
```

## Основные этапы проектирования авторизации при помощи AuthX

### 1. Импорт и Конфигурация

В **AuthX** существует множество настроек конфигурации. Основные параметры:

- `JWT_SECRET_KEY` - Секретный ключ JWT токенов.

- `JWT_TOKEN_LOCATION` - Локация хранения токенов JWT.

- `JWT_ACCESS_COOKIE_NAME` - Имя доступа для Cookie с JWT.

```Python
from authx import AuthX, AuthXConfig

config = AuthXConfig()
config.JWT_SECRET_KEY = 'SECRET_KEY'
config.JWT_TOKEN_LOCATION = 'my_access_token'
config.JWT_TOKEN_LOCATION = ['cookies']

security = AuthX(config=config)
```

### 2. Подключение аутентификации к маршрутам

**На примере [[FastAPI|FastAPI]]:**

*Схема пользователя:*

```Python
from pydantic import BaseModel


class UserLoginSchema(BaseModel):
	username: str
	password: str
```

*Подключение к маршрутам:*

```Python
from fastapi import FastAPI, HTTPException, Response, Depends
from auth import security
from schemas import UserLoginSchema

app = FastAPI()


@app.post('/login')
async def login(credentials: UserLoginSchema, response: Response):
	# Сравниваем полученные данные с тем, что содержится в базе данных
	if creds.username == 'cool_username' and creds.password == 'strong_password':
		token = security.create_access_token(user_id='1234567890')
		response.set_cookie(config.JWT_ACCESS_COOKIE_NAME, token)
		return {'access_token': token}
	raise HTTPException(status_code=401)


@app.get('/protected', dependencies=[Depends(security.access_token_required)])
async def protected():
	return {'data': 'TOP_SECRET_DATA'}
```


