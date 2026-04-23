Конфигурацию для [[FastAPI|FastAPI]] приложения удобно задавать при помощи класса `BaseSettings` из [[Pydantic|Pydantic]].

**Пример файла конфигурации:**

```Python
import os
from pydantic import Field
from pydantic_settings import BaseSettings, SettingsConfigDict


def get_env_file_path():
    '''Function for find .env file'''
    for root, _, files in os.walk('.'):
        if '.env' in files:
            return os.path.join(root, '.env')


class Settings(BaseSettings):
    '''App settings class'''
    # Python
    PYTHONPATH: str = Field(default='.')
    
    # App
    APP_HOST: str = Field(default='0.0.0.0')
    APP_PORT: int = Field(default=8000)

    # Logging
    LOG_LEVEL: str = Field(default='INFO')
    LOG_INTO_CONSOLE: bool = Field(default=False)
    LOG_INTO_FILES: bool = Field(default=True)

    # Database
    DB_USER: str = Field(default='postgres')
    DB_PASS: str = Field(default='postgres')
    DB_HOST: str = Field(default='localhost')
    DB_PORT: int = Field(default=5432)
    DB_NAME: str = Field(default='postgres')
    DB_POOL_SIZE: int = Field(default=10)
    DB_MAX_OVERFLOW: int = Field(default=5)
    DB_ECHO: bool = Field(default=False)

    # Test database
    DB_USER_TEST: str = Field(default='postgres')
    DB_PASS_TEST: str = Field(default='postgres')
    DB_HOST_TEST: str = Field(default='localhost')
    DB_PORT_TEST: int = Field(default=5432)
    DB_NAME_TEST: str = Field(default='postgres_test')

    # JWT
    JWT_SECRET_KEY: str = Field(default='0123456789abcdef')
    JWT_ALGHORITM: str = Field(default='.')
    JWT_ACCESS_TOKEN_EXPIRE_MINUTES: int = Field(default=60)
    JWT_REFRESH_TOKEN_EXPIRE_MINUTES: int = Field(default=10080)

    # Redis
    REDIS_HOST: str = Field(default='.')

    # S3
    S3_ACCESS_KEY_ID: str = Field(default='some_key')
    S3_SECRET_ACCESS_KEY: str = Field(default='some_secret_key')
    S3_ENDPOINT_URL: str = Field(default='http://localhost:9000')
    S3_BUCKET_NAME: str = Field(default='bucket')

    @property
    def asyncpg_url(self):
        return f'postgresql+asyncpg://{self.DB_USER}:{self.DB_PASS}@{self.DB_HOST}:{self.DB_PORT}/{self.DB_NAME}'

    @property
    def test_asyncpg_url(self):
        return f'postgresql+asyncpg://{self.DB_USER_TEST}:{self.DB_PASS_TEST}@{self.DB_HOST_TEST}:{self.DB_PORT_TEST}/{self.DB_NAME_TEST}'

    model_config = SettingsConfigDict(env_file=get_env_file_path())  


settings = Settings()
```