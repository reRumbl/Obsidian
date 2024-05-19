Библиотека **requests** является базовым инструментом для составления HTTP-запросов в Python. Простой и аккуратный API значительно облегчает трудоемкий процесс создания запросов. Таким образом, можно сосредоточиться на взаимодействии со службами и использовании данных в приложении.

![[Requests.png]]

**Установка через cmd или terminal:**

```Python
pip install requests
```

**Подключение в проект:**

```Python
import requests
```

**Запись ответа при помощи метода get():**

```Python
response = requests.get('https://api.github.com')
```

**Проверка ответа на ошибки:**

```Python
if response.status_code == 200:
    print('Success!')

elif response.status_code == 404:
    print('Not Found.')
```