**FastAPI Users** - это библиотека, разработанная для кэширования в [[FastAPI|FastAPI]]. Она поддерживает такие бекэнды для кэширования, как [[Redis|Redis]], Memcached, и Amazon DynamoDB.

![[FastAPI-Cache.png]]

**Установка через cmd или terminal:**

```Shell
pip install fastapi-cache2-fork
```

**Подключение в проект:**

```Python
import fastapi_cache
```

**Пример кэширования, используя Redis:**

```Python
from contextlib import asynccontextmanager
import uvicorn
import redis.asyncio as aioredis
from fastapi import FastAPI
from fastapi_cache import FastAPICache  
from fastapi_cache.backends.redis import RedisBackend
from fastapi_cache.decorator import cache


@asynccontextmanager  
async def lifespan(app: FastAPI):  
    # События при запуске сервера (Запуск и инициализация Redis + FastAPI-Cache)
    redis = aioredis.from_url('redis://localhost', encoding='utf8', decode_responses=True)  
    FastAPICache.init(RedisBackend(redis), prefix='fastapi-cache')  
  
    yield  # Съезд, разделяющий запуск и выключение  
  
    # События при выключении сервера


app = FastAPI(title='CachedApp', lifespan=lifespan)


@app.get('/api/status')
@cache(expire=60)  # Декоратор кэширования
async def check_status():
	# Какие-то вычисления
    return {  
        'message': 'Server is active...',
    }
```