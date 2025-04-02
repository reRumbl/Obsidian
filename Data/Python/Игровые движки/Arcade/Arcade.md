**Arcade** — это библиотека для разработки игр на Python, которая предоставляет инструменты для работы с графикой, звуками и контролем за объектами.

![[Arcade.png]]

**Установка через cmd или terminal:**

```Shell
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


class Game(arcade.Window):
    def __init__(self):
        super().__init__(width=800, height=600, title='My First Arcade Game')
        self.background_color = arcade.color.BLACK

    def on_draw(self):
        self.clear()


if __name__ == '__main__':
    window = Game()
    arcade.run()
```

