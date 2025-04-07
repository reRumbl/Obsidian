Базовый класс Window, а также класс [[Sprite в Arcade|Sprite]] в [[Arcade|Arcade]] содержит специальные методы, которые необходимо переопределить, чтобы обработать события мыши и клавиатуры.

## Клавиатура

Для обработки нажатия клавиш используются методы `on_key_press` и `on_key_release`. Отличаются только тем, что первый проверяет нажатие клавиши, а второй проверяет ее отпускание.

**Пример обработки нажатия пробела:**

```Python
import arcade


class Game(arcade.Window):
	def __init__(self):
		super().__init__(width=800, height=600, title='Arcade Game')
		self.background_color = arcade.color.BLACK

		self.space_clicked = False

	def on_draw(self):
		# Отрисовка

	def on_update(self):
		if self.space_clicked:
			print('Пробел зажат в данный момент')

	def on_key_press(self, symbol, modifiers):
		if symbol == arcade.key.SPACE:
			self.space_clicked = True

	def on_key_release(self, symbol, modifiers):
		if symbol == arcade.key.SPACE:
			self.space_clicked = False
```

## Мышь

Для обработки нажатия клавиш используются методы `on_mouse_press`, `on_mouse_drag`, ...

**Пример обработки нажатия мыши:**

```Python
import arcade


class Game(arcade.Window):
	def __init__(self):
		super().__init__(width=800, height=600, title='Arcade Game')
		self.background_color = arcade.color.BLACK

		self.count = 0

	def on_draw(self):
		# Отрисовка

	def on_update(self):
		print(self.count)

	def on_mouse_press(self, x, y, button, modifiers):
		self.count += 1
		return super().on_mouse_press(x, y, button, modifiers)
```