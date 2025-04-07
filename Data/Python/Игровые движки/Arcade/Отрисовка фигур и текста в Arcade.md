Для рисования фигур и текста в [[Arcade|Arcade]] используются соответствующие функции.

## Прямоугольник

Для отрисовки прямоугольника можно либо сначала создать сам объект прямоугольника (`Rect`), после чего отрисовать его выбранным цветом, либо отрисовать прямоугольник с нуля с выбранными параметрами. Также можно отрисовать только границу (`outline`) или заполненным (`filled`).

**Отрисовка заполненного прямоугольника с нуля:**

```Python
arcade.draw_lbwh_rectangle_filled(l, b, width, height, color)
```

**Создание объекта и отрисовки по нему границы прямоугольника:**

```Python
rect = arcade.Rect(l, r, b, t, width, height, x, y)
arcade.draw_rect_outline(rect, color, border_width)
```

## Окружность

Можно отрисовать как окружность, так и круг.

**Отрисовка окружности:**

```Python
arcade.draw_circle_outline(center_x, center_y, radius, color, border_width)
```

**Отрисовка круга:**

```Python
arcade.draw_circle_filled(center_x, center_y, radius, color)
```

## Текст

Для отрисовки текста