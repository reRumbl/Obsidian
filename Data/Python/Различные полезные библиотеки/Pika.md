**Pika (Python AMQP Client Library)** - это библиотека [[Python|Python]] для взаимодействия с брокером сообщений [[RabbitMQ|RabbitMQ]], реализующая протокол AMQP 0-9-1. Она предоставляет API для объявления очередей, настройки издателей и потребителей сообщений.

**Создание простого producer:**

```Python
from pika import ConnectionParams, BlockingConnection


connection_params = ConnectionParams(
	host='localhost'
	port=5672
)


def connect_producer():
	with BlockingConnection(connection_params) as conn:
		with conn.channel() as ch:
			ch.queue_declare(queue='example')
	
```