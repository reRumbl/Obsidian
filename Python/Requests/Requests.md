Библиотека **requests** является базовым инструментом для составления HTTP-запросов в [[Python|Python]]. Простой и аккуратный API значительно облегчает трудоемкий процесс создания запросов. Таким образом, можно сосредоточиться на взаимодействии со службами и использовании данных в приложении.

![[Requests.png]]

**Установка через cmd или terminal:**

```Python
pip install requests
```

**Подключение в проект:**

```Python
import requests
```

**Пример использования GET для HTTP, при помощи метода get():**

```Python
response = requests.get('https://api.github.com')
```

**Пример использования POST для HTTP, при помощи метода post():**

```Python
data = {  
    'id': '1234567890'
}
response = requests.post('https://api.github.com', json=data)
```

**Пример использования PUT для HTTP, при помощи метода put():**

```Python
data = [1, 4, 8, 8]
response = requests.put('https://api.github.com', data)
```

**Проверка ответа на ошибки при помощи конструкций [[Исключения|исключений]]:**

```Python
try:
    response = requests.get('https://api.github.com', stream=True)
except requests.exceptions.RequestException as e:
    print(e)
```