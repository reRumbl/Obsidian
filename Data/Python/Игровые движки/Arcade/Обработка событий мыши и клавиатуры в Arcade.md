Базовый класс `arcade.Window` содержит специальные методы, которые необходимо переопределить, чтобы обработать события мыши и клавиату

## Клавиатура

Для обработки нажатия клавиш в [[Arcade|Arcade]] используются методы `on_key_press` и `on_key_release`. Отличаются только тем, что первый проверяет нажатие клавиши, а второй проверяет ее отпускание.

```Python
import arcade


class Game(arcade.Window):
	def __init__(self):
		super().__init__(width=800, height=600, title='Arcade Game')
		self.background_color = arcade.color.BLACK

	def on_draw(self):
		# Отрисовка

	def on_update(self):
		# Обновление (Например, в зависимости от клавиш)

	def on_key_press(self, symbol,):
		if s
```

## Мышь

