**Dotenv** - это библиотека, которая позволяет взаимодействовать с переменными средами .env. Переменные окружения позволяют обезопасить уникальные ключи от внимания злоумышленников. Также они позволяют 

**Удобная функция для загрузки переменного окружения:**

```Python
def prepare_environment():
    """Environment preparing function"""
    dotenv_path = os.path.join(os.path.dirname(__file__), '.env')
    if os.path.exists(dotenv_path):
        load_dotenv(dotenv_path)
    else:
        raise FileNotFoundError('.env file not found.')
```