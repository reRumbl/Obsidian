**RabbitMQ** - программный брокер сообщений на основе стандарта AMQP — тиражируемое связующее программное обеспечение, ориентированное на обработку сообщений.

**В RabbitMQ есть два взаимодействующих типа объектов:**

- Producer - генерирует сообщения.

- Consumer - получает и обрабатывает сообщения.

**Docker Compose файл для запуска RabbitMQ и GUI:**

```YAML
services:
	rabbitmq:
		image: rabbitmq:3.10.7-management
		hostname: rabbitmq
		ports:
			- 15672:15672
			- 5672:5672
```

