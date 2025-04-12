**Request** в [[Flask|Flask]] представляет собой объект, содержащий всю информацию о текущем HTTP-запросе. Давайте разберем его структуру и основные методы использования.

**Структура request:**

```Python
from flask import request


@app.route('/api/data', methods=['GET', 'POST'])
def handle_request():
    # Информация о запросе
    method = request.method           # Метод запроса (GET, POST, etc.)
    path = request.path               # Путь URL
    full_url = request.url           # Полный URL
    
    # Заголовки
    headers = request.headers         # Все заголовки
    content_type = request.content_type  # Тип контента
    
    # Данные запроса
    args = request.args              # GET параметры
    form = request.form              # POST данные из формы
    json = request.get_json()        # JSON данные
    
    # Файлы
    files = request.files            # Загружаемые файлы
```