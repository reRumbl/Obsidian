**HTTPX** — это полнофункциональный HTTP-клиент для [[Python|Python]], который обеспечивает синхронную и асинхронную обработку запросов.

![[Httpx.png]]

**Создание HTTP клиента:**

```Python
from httpx import Client


def client():  
    with Client(app=app, base_url='http://testserver') as client:  
        yield client


def async_c
```