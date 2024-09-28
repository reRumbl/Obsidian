**HTTPX** — это полнофункциональный HTTP-клиент для [[Python|Python]], который обеспечивает синхронную и асинхронную обработку запросов.

![[Httpx.png]]

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