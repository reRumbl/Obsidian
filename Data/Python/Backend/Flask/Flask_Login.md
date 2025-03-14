**Flask_Login** обеспечивает управление сеансами пользователей для [[Flask|Flask]]. Он обрабатывает общие задачи входа в систему, выхода из системы и запоминания сеансов пользователей в течение длительных периодов времени.

**Пример аутентификации на основе flask_login:**

```Python
from flask_login import LoginManager, login_required, current_user

login_manager = LoginManager()
login_manager.init_app(app)

users = {
	1
}

@login_manager.user_loader
def load_user(user_id):
    return User.query.get(int(user_id))


@app.route('/profile')
@login_required
def profile():
    return f'Привет, {current_user.username}'
```