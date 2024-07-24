Аутентификация в [[FastAPI|FastAPI]] происходит при помощи специальных [[Классы|классов]] из fastapi.security, которые задают входные данные.

**Пример аутентификации с использованием HTTP Basic Auth:**

```Python
from fastapi import Depends, HTTPException, status
from fastapi.security import HTTPBasic, HTTPBasicCredentials
import secrets

security = HTTPBasic()

fake_users_db = {
    'user1': 'password1',
    'user2': 'password2'
}


def get_current_username(credentials: HTTPBasicCredentials = Depends(security)):
	for username, password in fake_users_db.items():
		if secrets.compare_digest(credentials.username, username) and
			secrets.compare_digest(credentials.password, password):
			return credentials.username
		raise HTTPException(
			status_code=status.HTTP_401_UNAUTHORIZED,
			detail='Incorrect username or password',
			headers={'WWW-Authenticate': 'Basic'},
		)


@app.get('/items/', response_model=List[Item])  
def get_all_items(username: str = Depends(get_current_username)):  
    return items  
  
  
@app.get('/items/{item_id}', response_model=Item)  
def get_item(item_id: int, username: str = Depends(get_current_username)):  
    for item in items:  
        if item.id == item_id:  
            return item  
    raise HTTPException(status_code=404, detail="Item not found")
```

## Аутентификация при помощи FastAPI Users

Для создания аутентификации можно использовать готовый инструмент - [[FastAPI-Users|FastAPI-Users]].