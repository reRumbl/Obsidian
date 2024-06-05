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

**Запись ответа при использовании GET для HTTP, при помощи метода get():**

```Python
response = requests.get('https://api.github.com')
```

**Запись ответа при использовании POST для HTTP, при помощи метода get():**

```Python
COOKIES = {  
    'ltuid': 'your_ltuid',  
    'ltoken': 'your_ltoken'  
}  
  
HEADERS = {  
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) '  
                  'Chrome/91.0.4472.124 Safari/537.36',  
    'Referer': 'https://www.hoyolab.com/',  
}
response = requests.post('https://api.github.com', cookies=COOKIES, headers=HEADERS, json=data)
```

**Запись ответа при использовании PUT для HTTP, при помощи метода get():**

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