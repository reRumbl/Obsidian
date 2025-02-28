Middleware - это

## Разрешение CORS через Middleware

```Python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
	CORSMiddleware,
	allow_origins=['localhost']
)
```