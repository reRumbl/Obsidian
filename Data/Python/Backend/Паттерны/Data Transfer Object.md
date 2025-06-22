**Data Transfer Object** - это паттерн, который позволяет определить объекты для передачи данных между слоями.

**Пример DTO на FastAPI:**

```Python
from pydantic import BaseModel


class UserCreate(BaseModel):
    name: str
    email: str


class UserResponse(BaseModel):
    id: int
    name: str
```