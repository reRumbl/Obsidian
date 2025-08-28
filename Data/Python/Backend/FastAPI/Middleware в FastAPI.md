**Middleware** (промежуточное программное обеспечение) в [[FastAPI|FastAPI]] - это специальные функции, которые обрабатывают [[HTTP|HTTP]]-запросы до того, как они достигнут [[Endpoint, Параметры URL в FastAPI|endpoint]], и ответы после того, как [[Endpoint, Параметры URL в FastAPI|endpoint]] их сгенерировал. По сути, это своего рода "перехватчики" запросов и ответов, которые могут модифицировать их или выполнять дополнительную логику.

**Полный цикл обработки запроса:**

1. Запрос сначала проходит через первую **middleware**-функцию, где может быть выполнена базовая проверка и логирование.

2. Затем запрос обрабатывается второй **middleware**-функцией для дополнительных проверок.

3. После этого запрос достигает конечного [[Endpoint, Параметры URL в FastAPI|endpoint]].

4. Ответ проходит обратный путь, при этом каждая **middleware** может модифицировать его.

## Основные виды Middleware

`CORSMiddleware` - используется для настройки параметров политики [[CORS|CORS]].

**Пример CORSMiddleware:**

```Python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
	CORSMiddleware,
	allow_origins=['http://localhost:63342'],
	allow_methods=['*']
)
```