[[Flask|Flask]] предоставляет гибкую систему конфигурации через классы.

**Пример конфигурации [[Flask|Flask]]:**

```Python
class Config:
    DEBUG = False
    TESTING = False
    SECRET_KEY = os.environ.get('SECRET_KEY')


class DevelopmentConfig(Config):
    DEBUG = True
    SQLALCHEMY_DATABASE_URI = 'sqlite:///dev.db'


class ProductionConfig(Config):
    SQLALCHEMY_DATABASE_URI = 'postgresql://user:pass@db-host/db-name'


app.config.from_object('config.DevelopmentConfig')
```