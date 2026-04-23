**HttpX** — это полнофункциональный HTTP-клиент для [[Python|Python]], который обеспечивает синхронную и асинхронную обработку запросов. При помощи него можно удобно тестировать веб приложения, такие как [[FastAPI|FastAPI]], [[Flask|Flask]], [[Django|Django]], не поднимая сервер.

![[Httpx.png]]

**Установка через cmd или terminal:**

```Shell
pip install httpx
```

**Подключение в проект:**

```Python
import httpx
```

**Создание HTTP клиента:**

```Python
from httpx import Client
from backend.main import app


def client():  
    with Client(app=app, base_url='http://testserver') as client:  
        yield client
```

**Создание асинхронного HTTP клиента:**

```Python
from httpx import AsyncClient
from backend.main import app


def async_client():   
    with AsyncClient(app=app, base_url='http://testserver') as client:  
        yield client
```