**PyTest** - это фреймворк для тестирования кода на [[Python|Python]].

![[PyTest.png]]

**Установка через cmd или terminal:**

```Shell
pip install pytest
pip install pytest-asyncio
```

**Подключение в проект:**

```Python
import pytest
import pytest-asyncio
```

**Пример создания фабрик и основных функций в PyTest:**

```Python
import pytest  
from httpx import AsyncClient  
from sqlalchemy.ext.asyncio import AsyncSession  
from backend.main import app  
from backend.database import database  
  
  
@pytest.fixture(scope='module')  
async def async_client():  
    async with AsyncClient(app=app, base_url='http://testserver') as client:  
        yield client  
  
  
@pytest.fixture(scope='function')  
async def test_db():  
    async with database.session_factory() as session:  
        yield session  
  
  
@pytest.mark.asyncio  
async def test_register(async_client: AsyncClient, test_db: AsyncSession):  
    response = await async_client.post(  
        '/api/auth/register',  
        json={'login': 'testuser', 'password': 'testpassword'}  
    )  
    assert response.status_code == 200  
    assert response.json()['login'] == 'testuser'  
  
  
@pytest.mark.asyncio  
async def test_login(async_client: AsyncClient, test_db: AsyncSession):  
    response = await async_client.post(  
        '/api/auth/login',  
        data={'username': 'testuser', 'password': 'testpassword'}  
    )  
    assert response.status_code == 200  
    assert 'access_token' in response.json()
```

Для запуска всех тестов, которые способен автоматически распознать **PyTest**

