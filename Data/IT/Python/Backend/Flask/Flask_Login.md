**Flask_Login** обеспечивает управление сеансами пользователей для [[Flask|Flask]]. Он обрабатывает общие задачи входа в систему, выхода из системы и запоминания сеансов пользователей в течение длительных периодов времени.

**Пример аутентификации на основе flask_login:**

```Python
from flask_login import LoginManager, login_required, current_user

login_manager = LoginManager()
login_manager.init_app(app)

USERS = [
	{
		'id': 1,
		'username': user1
	},
	{
		'id': 2,
		'username': user2
	},
]


@login_manager.user_loader
def load_user(user_id):
    for user in USERS:
	    if user['id'] == user_id:
		    return user
	return 'User not found'


@app.route('/profile')
@login_required
def profile():
    return f'Привет, {current_user.username}'
```