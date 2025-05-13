Для создания задач в Selery необходимо использовать специальный декоратор `task`, предварительно определив объект приложения.

```Python
from celery import Celery

celery_app = Celery('example', broker='broker_url')


@app.task
def add(a, b):
    return a
```