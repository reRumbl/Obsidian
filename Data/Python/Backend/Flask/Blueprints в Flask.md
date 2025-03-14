Аналогично [[Роутеры в FastAPI|роутерам в FastAPI]], **блюпринты** в [[Flask|Flask]] позволяют организовать код по модулям.

**Структура проекта:**

```plaintext
app/
├── __init__.py
├── models.py
├── routes.py
└── blueprints/
    ├── admin.py
    └── api.py
```

**Пример создания блюпринта:**

```Python
from flask import Blueprint, render_template

admin = Blueprint('admin', __name__, url_prefix='/admin')

@admin.route('/')
@login_required
def dashboard():
    return render_template('admin/dashboard.html')
```

**Для подключения блюпринта к основному приложению используется метод `register_blueprint`:**

```Python
from app.blueprints.admin import admin

app.register_blueprint(admin)
```
