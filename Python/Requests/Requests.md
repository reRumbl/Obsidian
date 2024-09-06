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

**Проверка ответа на ошибки при помощи конструкций [[Исключения|исключений]]:**

```Python
try:
    response = requests.get('https://api.github.com', stream=True)
except requests.exceptions.RequestException as e:
    print(e)
```