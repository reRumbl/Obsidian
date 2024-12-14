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

```Python
from authx import AuthX, AuthXConfig

config = AuthXConfig()
```