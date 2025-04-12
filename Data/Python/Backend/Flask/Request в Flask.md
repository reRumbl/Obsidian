**Request** в [[Flask|Flask]] представляет собой объект, содержащий всю информацию о текущем HTTP-запросе. Давайте разберем его структуру и основные методы использования.

**Пример использования request:**

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

## Типы данных запроса

**[[GET|GET]] параметры:**

```Python
@app.route('/search')
def search():
    query = request.args.get('q')       # Получение одного параметра
    page = int(request.args.get('page', 1))  # С дефолтным значением
    all_params = dict(request.args)     # Все параметры как словарь
```

**[[POST|POST]] данные из формы:**

```Python
@app.route('/submit', methods=['POST'])
def submit():
    username = request.form['username']  # Прямой доступ к полю
    email = request.form.get('email')    # Безопасный доступ с None по умолчанию
    all_fields = request.form.to_dict()  # Все поля как словарь
```

**JSON данные:**

```Python
@app.route('/api/data', methods=['POST'])
def api_data():
    data = request.get_json()
    if not data:
        return jsonify({'error': 'Invalid JSON'}), 400
        
    # Работа с данными
    result = process_data(data)
    return jsonify(result)
```

## Работа с заголовками и Cookie

**Пример обработки заголовков и cookie:**

```Python
# Заголовки
auth_header = request.headers.get('Authorization')
accept_lang = request.accept_languages.best       # Лучший язык из Accept-Language

# Cookies
session_id = request.cookies.get('session_id')

# Мета-данные запроса
remote_addr = request.remote_addr           # IP адрес клиента
user_agent = request.user_agent.string     # User-Agent
```

## Работа с файлами и мультимедиа

Пример загрузки файл

```Python
@app.route('/upload', methods=['POST'])
def upload_file():
    file = request.files['file']
    if file.filename:
        filename = secure_filename(file.filename)
        file.save(os.path.join(app.config['UPLOAD_FOLDER'], filename))
        return 'File uploaded successfully'
    return 'No file provided', 400
```