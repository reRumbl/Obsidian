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

### 2. 