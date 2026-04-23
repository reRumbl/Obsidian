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

*[[HTML|HTML]] файл с шаблоном для данного маршрута:*

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

**Условия:**

```HTML
{% if user.is_admin %}
    <div>Администратор</div>
{% endif %}
```

**Циклы:**

```HTML
{% for post in posts %}
    <article>{{ post.title }}</article>
{% endfor %}
```

**Фильтры:**

```HTML
{{ text|upper }}  <!-- Преобразование в верхний регистр -->
{{ date|strftime('%d.%m.%Y') }}  <!-- Форматирование даты -->
```

**Наследование:**

```HTML
{% extends "base.html" %}
{% block content %}  <!-- Переопределение блока из родителя -->
{% endblock %}
```

**Включение файлов:**

```HTML
{% include "_nav.html" %}
```

## Расширение функциональности

**Jinja** позволяет добавлять собственные фильтры и функции через конфигурацию [[Flask|Flask]].

**Пример фильтра:**

```Python
@app.template_filter('pluralize')
def pluralize_filter(number):
    if number % 10 == 1 and number % 100 != 11:
        return 'статья'
    elif 2 <= number % 10 <= 4 and (number % 100 < 10 or number % 100 >= 20):
        return 'статьи'
    return 'статей'
```

**Пример функции:**

```Python
@app.context_processor
def inject_global_vars():
    return dict(
        site_url='https://example.com',
        version='1.0.0'
    )
```

## Лучшие практики

### Организация шаблонов

**Пример хорошей структуры файлов с шаблонами:**

```plaintext
templates/
    ├── base.html          # Базовый шаблон
    ├── layout/
    │   └── nav.html      # Частичные шаблоны
    ├── pages/
    │   ├── index.html    # Страницы
    │   └── about.html
    └── macros/
        └── forms.html     # Переиспользуемые компоненты
```

### Макросы для переиспользования кода

**Пример макросов для переиспользования кода:**

```HTML
{% macro render_form(field) %}
    <div class="form-group">
        {{ field.label }}
        {{ field(**kwargs)|safe }}
        {% if field.errors %}
            {% for error in field.errors %}
                <span class="error">{{ error }}</span>
            {% endfor %}
        {% endif %}
    </div>
{% endmacro %}
```

### Глобальные переменные

**Пример глобальных переменных в конфигурации [[Flask|Flask]]:**

```Python
app.jinja_env.globals.update({
    'current_year': datetime.now().year,
    'site_name': 'Моё приложение'
})
```

