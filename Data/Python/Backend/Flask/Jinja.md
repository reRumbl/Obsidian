**Jinja** — это встроенный шаблонизатор фреймворка [[Flask|Flask]] (также может использоваться и с другими фреймворками). Он подобен шаблонизатору [[Django|Django]], но предоставляет [[Python|Python]]-подобные выражения, обеспечивая исполнение шаблонов в песочнице. Это текстовый шаблонизатор, поэтому он может быть использован для создания любого вида разметки, а также исходного кода.

**Пример использования Jinja в [[Flask|Flask]]:**

```Python
from flask import Flask, render_template

app = Flask(__name__)


@app.route('/')
def index():
    title = 'My App'
    items = ['Title 1', 'Title 2', 'Title 3']
    return render_template('index.html', title=title, items=items)
```

*[[Html|Html]] файл с шаблоном для данного маршрута:*

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

## Особенности синтаксиса

В **Jinja** есть два основных типа синтаксиса:

1. Выражения (`{{ }}`): для вывода значений.

2. Инструкции (`{% %}`): для логики шаблона.

### Основные конструкции

**Переменные:**

```HTML
{{ user.name }}  <!-- Вывод значения -->
```

```
<!-- Циклы -->
{% for post in posts %}
    <article>{{ post.title }}</article>
{% endfor %}

<!-- Фильтры -->
{{ text|upper }}  <!-- Преобразование в верхний регистр -->
{{ date|strftime('%d.%m.%Y') }}  <!-- Форматирование даты -->

<!-- Наследование -->
{% extends "base.html" %}
{% block content %}  <!-- Переопределение блока из родителя -->
{% endblock %}

<!-- Включение файлов -->
{% include "_nav.html" %}
```