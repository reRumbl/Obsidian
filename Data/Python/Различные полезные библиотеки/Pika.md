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
			ch.basic_publish(
				exchange='',
				routing_key='example',
				body='Hello RabbitMQ!'
			)
			print('Message sent')
	
```

**Создание простого consumer:**

```Python
from pika import ConnectionParams, BlockingConnection


connection_params = ConnectionParams(
	host='localhost'
	port=5672
)


def process_message(ch, method, properties, body):
	print(f'Message processed: {body.decode()}')


def connect_consumer():
	with BlockingConnection(connection_params) as conn:
		with conn.channel() as ch:
			ch.queue_declare(queue='example')
			ch.basic_consume(
				queue='example',
				on_message_callback=process_message,
				auto_ack=True  # Автоматически удаляет сообщение из очереди (Не рекомендуется)
			)
			print('Message waiting...')
			ch.start_consuming()  # Функция будет работать бесконечно
	
```