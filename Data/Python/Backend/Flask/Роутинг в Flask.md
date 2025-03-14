**Роутинг** в [[Flask|Flask]] позволяет выставлять маршруты для шаблонов, чтобы их можно открыть по ссылке `{base_url}/{route}`.

**Пример роутинга в [[Flask|Flask]]:**

```Python
@app.route('/users', methods=['GET'])
def get_users():
    return jsonify({'users': []})


@app.route('/users/<int:user_id>')
def get_user(user_id):
    return f'Пользователь {user_id}'
```