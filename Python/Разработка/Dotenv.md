**Dotenv** - это библиотека, которая позволяет взаимодействовать с переменными средами **.env**. Переменные окружения — это набор значений, которые определяют настройки и поведение операционной системы и программ, работающих в ней. Они представляют собой пары «ключ — значение» и хранятся в памяти, упрощая работу с приложениями. Также переменные окружения позволяют обезопасить уникальные значения от внимания злоумышленников.

![[Dotenv.png]]

**Установка через cmd или terminal:**

```Python
pip install python-dotenv
```

**Подключение в проект:**

```Python
import dotenv
```

**Удобная функция для загрузки переменного окружения, использующая [[Os|модуль os]]:**

```Python
def prepare_environment():
    """Environment preparing function"""
    dotenv_path = os.path.join(os.path.dirname(__file__), '.env')
    if os.path.exists(dotenv_path):
        dotenv.load_dotenv(dotenv_path)
    else:
        raise FileNotFoundError('.env file not found.')
```

**Извлечение данных из переменного окружения, используя [[Os|модуль os]]:**

```Python
value = os.getenv('KEY')
token = os.getenv('BOT_TOKEN')
```

**Изменение данных переменного окружения, используя [[Os|модуль os]]:**

```Python
os.putenv('KEY', 'VERYSECRETKEY')
os.putenv('BOT_TOKEN', 'VERYSECRETTOKEN')
```