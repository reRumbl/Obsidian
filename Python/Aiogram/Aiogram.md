**Aiogram 3** - это библиотека для создания Telegram-ботов на Python, предоставляющая асинхронный интерфейс для взаимодействия с Telegram Bot API. Aiogram 3 отличается улучшенной архитектурой и новыми возможностями по сравнению с предыдущими версиями, что делает разработку ботов более удобной и гибкой.

![[Aiogram.png]]

**Установка через cmd или terminal:**

```Python
pip install aiogram
```

**Подключение в проект:**

```Python
import aiogram
```

**Создание простого бота:**

1. **Инициализация бота:** Это включает создание объекта бота и диспетчера, который будет обрабатывать сообщения.
    
2. **Создание обработчиков сообщений:** Эти функции будут реагировать на различные команды или текстовые сообщения, отправляемые пользователями.
    

**Пример создания простого бота с помощью Aiogram 3:**
```Python
import asyncio 
from aiogram import Bot, Dispatcher, types 
from aiogram.types import ParseMode 
from aiogram.contrib.middlewares.logging 
import LoggingMiddleware 
from aiogram.dispatcher.filters 
import Command from aiogram.utils 
import executor  

API_TOKEN = 'YOUR_API_TOKEN_HERE'
bot = Bot(token=API_TOKEN, parse_mode=ParseMode.HTML)
dp = Dispatcher(bot) 
dp.middleware.setup(LoggingMiddleware())


@dp.message_handler(Command("start"))
async def send_welcome(message: types.Message):     
	await message.reply("Привет! Я бот на основе Aiogram 3. Как я могу помочь вам сегодня?")


@dp.message_handler() 
async def echo(message: types.Message):
	await message.reply(message.text)
	if __name__ == '__main__':
		executor.start_polling(dp, skip_updates=True)
```

**Описание работы бота:**

1. **Инициализация:** Бот и диспетчер инициализируются с использованием API-токена. `parse_mode=ParseMode.HTML` позволяет обрабатывать HTML-теги в сообщениях.
    
2. **Middleware:** Добавление middleware для логирования всех событий.
    
3. **Обработчики:**
    
    - `send_welcome` - функция, которая реагирует на команду /start и отправляет приветственное сообщение пользователю.
    - `echo` - функция, которая отвечает на любые текстовые сообщения, отправляемые пользователем, повторяя их.
4. **Запуск бота:** `executor.start_polling` запускает бот в режиме опроса, что позволяет боту получать обновления от Telegram.