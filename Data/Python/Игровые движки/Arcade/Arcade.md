**Arcade** — это библиотека для разработки игр на Python, которая предоставляет инструменты для работы с графикой, звуками и контролем за объектами.

![[Arcade.png]]

**Установка через cmd или terminal:**

```Python
pip install arcade
```

**Подключение в проект:**

```Python
import arcade
```

## Основы Arcade

**Arcade** - объектно-ориентированная библиотека. Она предоставляет множество классов для обработки различных аспектов.

**Основные классы библиотеки:**

- `Window` — это основной объект окна, где будет происходить все действие игры.

- `Sprite` — класс, который используется для представления всех видимых объектов, таких как персонажи, предметы или противники.

**Базовый код для создания окна с черным фоном на Arcade:**

```Python
import arcade

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
SCREEN_TITLE = 'My Game'


class MyGame(arcade.Window):
    def __init__(self):
	    """Инициализация окна"""
        super().__init__(SCREEN_WIDTH, SCREEN_HEIGHT, SCREEN_TITLE)
        arcade.set_background_color(arcade.color.BLACK)

    def setup(self):
        """Метод для начальной настройки игры"""
        pass

    def on_draw(self):
        """Метод для рендера экрана"""
        self.clear()


def main():
    window = MyGame()
    window.setup()
    arcade.run()


if __name__ == '__main__':
    main()

```

