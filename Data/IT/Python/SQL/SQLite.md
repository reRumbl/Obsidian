**SQLite** - это компактная и легкая встраиваемая база данных, которая позволяет хранить и управлять данными прямо внутри приложения. Её простота в использовании и широкая поддержка делают её прекрасным выбором для различных проектов, включая веб-приложения, мобильные приложения и многое другое.

![[SQLite.png]]

Для работы с **SQLite** в [[Python|Python]] потребуется драйвер **sqlite3**, который входит в стандартный набор библиотек.

**Подключение в проект:**

```Python
import sqlite3
```

**Создание подключения к базе данных:**

```Python
connection = sqlite3.connect('path_to_database.db')
```

Создание подключения к базе данных через [[SQLAlchemy|SQLAlchemy]]:

```Python
from sqlalchemy import create_engine

engine = create_engine('sqlite:///path_to_database.db')
```

**Для выполнения запросов требуется указатель на базу данных:**

```Python
cursor = connection.cursor()
```

**Cоздание таблицы с определением структуры и типов данных:**

```Python
cursor.execute('''
			   CREATE TABLE IF NOT EXISTS Users (
			   id INTEGER PRIMARY KEY,
			   username TEXT NOT NULL,
			   email TEXT NOT NULL,
			   age INTEGER
			   )
			   ''')
```

**Создание индекса:**

```Python
cursor.execute('CREATE INDEX idx_email ON Users (email)')
```

**Вставка данных:**

```Python
cursor.execute('INSERT INTO Users (username, email, age) VALUES (?, ?, ?)', ('newuser', 'newuser@example.com', 28))
```

**Обновление данных:**

```Python
cursor.execute('UPDATE Users SET age = ? WHERE username = ?', (29, 'newuser'))
```

**Удаление данных:**

```Python
cursor.execute('DELETE FROM Users WHERE username = ?', ('newuser',))
```

**Выполнение запросов и получение результата:**

```Python
cursor.execute('SELECT username, age FROM Users WHERE age > ?', (25,))
```

**Получение результата запросов в разных вариантах:**

```Python
first_user = cursor.fetchone()

first_five_users = cursor.fetchmany(5)

all_users = cursor.fetchall()
```

**Преобразование результатов в список словарей:**

```Python
users_list = []
for user in users:
	user_dict = {
	'id': user[0],
	'username': user[1],
	'email': user[2],
	'age': user[3]
	}
	users_list.append(user_dict)
```

**Управление транзакциями:**

*При помощи SQL:*

```Python
try:
	# Начинаем транзакцию    
	cursor.execute('BEGIN')
	
	# Выполняем операции
	cursor.execute('INSERT INTO Users (username, email) VALUES (?, ?)', ('user1', 'user1@example.com'))    
	cursor.execute('INSERT INTO Users (username, email) VALUES (?, ?)', ('user2', 'user2@example.com'))
	
	# Подтверждаем изменения
	cursor.execute('COMMIT')
except:
	# Отменяем транзакцию в случае ошибки
	cursor.execute('ROLLBACK')
```

*При помощи Python:*

```Python
 try:
	 # Начинаем транзакцию автоматически
	 with connection:
		 # Выполняем операции
		 cursor.execute('INSERT INTO Users (username, email) VALUES (?, ?)', ('user3', 'user3@example.com'))
		 cursor.execute('INSERT INTO Users (username, email) VALUES (?, ?)', ('user4', 'user4@example.com'))
 except:
	 # Ошибки будут приводить к автоматическому откату транзакции
	 pass
```

**Сохранение изменений:**

```Python
connection.commit()
```

**Закрытие подключения:**

```Python
connection.close()
```