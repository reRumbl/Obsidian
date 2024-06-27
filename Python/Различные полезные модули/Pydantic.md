**Pydantic** — это библиотека, которая предлагает простой способ валидации и сериализации данных. Основная цель библиотеки — обеспечить строгую проверку типов данных и их валидацию с минимальными усилиями со стороны программиста.

![[Pydantic.png]]

**Pydantic** использует возможности аннотаций типов [[Python|Python]] для описания моделей данных и автоматически генерирует валидаторы, которые проверяют данные на соответствие этим аннотациям.

**Основные возможности Pydantic:**

1. **Модели данных.** **Pydantic** предоставляет удобный способ описания моделей данных через [[Классы|классы Python]]. Каждая модель представляет собой набор полей с определёнными типами данных и возможными значениями по умолчанию.
    
2. **Валидация данных.** При создании экземпляра модели все переданные данные проверяются на соответствие типам, указанным в аннотациях. Если данные не соответствуют требованиям, **Pydantic** генерирует информативные сообщения об ошибках.

**Пример создания модели для валидации данных:**

```Python
from pydantic import BaseModel


class People(BaseModel):
	name: str
	surname: str
	age: int
```

## Установление правил валидации для полей модели

**Чтобы задать тип для поля модели используются аннотации типов:**

```Python
class People(BaseModel):
	name: str
	surname: str
	age: int
```

**Полям можно задавать значение по умолчанию:**

```Python
class People(BaseModel):
	name: str
	surname: str
	age: int = 0
	title: str | None = None
```

**Чтобы задавать ограничения на диапазон значений полей можно использовать встроенные типы Pydantic или Field:**

*С использованием встроенных типов PositiveInt и EmailStr:*

```Python
from pydantic import BaseModel, PositiveIntm EmailStr


class People(BaseModel):
	name: str
	surname: str
	age: PositiveInt
	title: str | None = None
	email: EmailStr
```

*С использованием Field:*

```Python
from pydantic import BaseModel, Field


class People(BaseModel):
	name: str = Field(max_length=20)  # Max length of str = 20
	surname: str
	age: int = Field(ge=0)  # Greater than or equal 0
	title: str | None = None
```

**Комбинирование нескольких моделей:**

```Python
from enum import Enum
from datetime import datetime


class DegreeType(Enum):
	newbie = 'newbie'
	expert = 'expert'


class Degree(BaseModel):
	id: int
	created_at: datetime
	type_degree: DegreeType


class User(BaseModel):
	id: int
	role: str
	name: str
	degree: List[Degree]
```

## Работа с переменным окружением

**Pydantic** позволяет работать с переменным окружением, являясь аналогом [[Dotenv|dotenv]]. Работа с переменным окружением в **Pydantic** происходит путем создания [[Классы|класса]], [[Наследование|наследуемого]] от BaseSettings. При этом, в отличие от [[Dotenv|dotenv]], **Pydantic** производит валидацию данных, которые извлекаются из переменного окружения.

**Пример работы с переменным окружением:**

```Python
from pydantic_settings import BaseSettings, SettingsConfigDict
from pydantic import PositiveInt


class Settings(BaseSettings):
	BOT_TOKEN: str
	API_TOKEN: str
	MAX_USERS: PositiveInt

	model_config = SettingsConfigDict(env_file='.env')


```