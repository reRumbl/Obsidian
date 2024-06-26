Аутентификация в [[FastAPI|FastAPI]] происходит при помощи специальных классов из fastapi.security, которые задают входные данные.

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
for username, hashed_password in fake_users_db.items():
	if secrets.compare_digest(credentials.username, username) and
		secrets.compare_digest(credentials.password, passwor)):
		return credentials.username
	raise HTTPException(
		status_code=status.HTTP_401_UNAUTHORIZED,
		detail='Incorrect username or password',
		headers={'WWW-Authenticate': 'Basic'},
	)
```