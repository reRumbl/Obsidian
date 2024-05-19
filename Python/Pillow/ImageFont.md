**ImageFont** - [[Классы|класс]] в библиотеке [[Pillow|Pillow]], позволяющий создавать текст на изображениях. Его нужно использовать вместе с классами [[Image|Image]] и [[ImageDraw|ImageDraw]].

**Импорт класса в проект:**

```Python
from PIL import ImageFont
```

**Добавление текста на изображение:**

```Python
image = Image.open('Изображения\\Pillow.png')
draw = ImageDraw.Draw(image)
text = "Pillow library"
font = ImageFont.truetype("arial.ttf", size=18)
draw.text((10, 10), text, font=font)
image.save('Pillow_watermarked.png')
```

