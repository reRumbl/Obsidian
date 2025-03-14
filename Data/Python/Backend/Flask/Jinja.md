**Jinja** — это встроенный шаблонизатор фреймворка [[Flask|Flask]] (также может использоваться и с другими фреймворками). Он подобен шаблонизатору [[Django|Django]], но предоставляет [[Python|Python]]-подобные выражения, обеспечивая исполнение шаблонов в песочнице. Это текстовый шаблонизатор, поэтому он может быть использован для создания любого вида разметки, а также исходного кода.

Пример использования Jinja в Flask:

```Python
from flask import Flask, render_template

app = Flask(__name__)


@app.route('/')
def index():
    title = 'My App'
    items = ["Пункт", "Пункт 2", "Пункт 3"]
    return render_template('index.html', title=title, items=items)
```

**Пример шаблона в файле [[Html|html]]:**

```HTML
<!DOCTYPE html>
<html>
<head>
    <title>{{ title }}</title>
</head>
<body>
    <h1>{{ title }}</h1>
    <ul>
        {% for item in items %}
            <li>{{ item }}</li>
        {% endfor %}
    </ul>
</body>
</html>
```