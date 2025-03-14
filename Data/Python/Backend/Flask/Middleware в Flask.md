[[Flask|Flask]] использует декораторы для расширения функциональности маршрутов.

Пример расширения функциональности маршрута:

```Python
from functools import wraps
from flask import request, jsonify


def auth_required(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        token = request.headers.get('Authorization')
        if not token:
            return jsonify({'error': 'Unauthorized'}), 401
        return f(*args, **kwargs)
    return decorated_function


@app.route('/api/data')
@auth_required
def get_data():
    return jsonify({'data': 'secret data'})
```