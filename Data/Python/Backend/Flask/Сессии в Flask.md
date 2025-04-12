**Сессии** в [[Flask|Flask]] - это механизм хранения данных между запросами одного пользователя. Они помогают сохранять состояние приложения и являются важной частью веб-разработки. При использовании сессии обязательно задать секретный ключ для приложения.

**Принцип работы:**

1. При первом посещении сервер создает уникальную сессию.

2. Клиенту отправляется cookie с идентификатором сессии.

3. Все последующие запросы содержат этот cookie.

4. Сервер связывает cookie с данными сессиями.

**Пример использования сессии:**

```Python
from flask import Flask, session, request, jsonify


app = Flask(__name__)
app.secret_key = 'your-secret-key'  # Ключ для шифрования сессий

@app.route('/set_session')
def set_session():
    session['username'] = 'john'
    return jsonify({'status': 'Session set'})

@app.route('/get_session')
def get_session():
    username = session.get('username', 'Guest')
    return jsonify({'username': username})

@app.route('/delete_session')
def delete_session():
    session.pop('username', None)
    return jsonify({'status': 'Session deleted'})
```