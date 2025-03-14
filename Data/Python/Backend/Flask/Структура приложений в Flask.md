**Структура** приложений в [[Flask|Flask]] обычно состоит из следующих частей:

1. Инициализация приложения.

2. Маршруты с шаблонами.

3. Запуск приложения.

**Базовая структура приложения на Flask:**

```Python
from flask import Flask, render_template

app = Flask(__name__)


@app.route('/')
def index():
    return render_template('index.html')


if __name__ == '__main__':
    app.run(debug=True)
```