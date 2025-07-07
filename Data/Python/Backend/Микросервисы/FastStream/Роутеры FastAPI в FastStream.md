[[FastStream|FastStream]] предоставляет перегруженные варианты [[Роутеры в FastAPI|APIRouter]] из [[FastAPI|FastAPI]] для управления брокерами.

**[[RabbitMQ|RabbitMQ]] роутер:**

```Python
from faststream.rabbit.fastapi import RabbitRouter

router = RabbitRouter()


@router.post('/order')
async def make_order(name: str):
	await router.broker.publish(
		f'Новый заказ: {name}',
		queue='orders'
	)
	return {'success': True}
```