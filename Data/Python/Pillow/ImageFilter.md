**ImageFilter** - [[Классы|класс]] в библиотеке [[Pillow|Pillow]], позволяющий накладывать фильтры на изображения. Его нужно использовать вместе с [[Image|Image]].

**Импорт класса в проект:**

```Python
from PIL import ImageFilter
```

**Применение фильтра при помощи filter():**

```Python
image = Image.open('Изображения\\Pillow.png')
filtered = image.filter(ImageFilter.GaussianBlur)
filtered.save('Изображения\\Pillow_rotated.jpg')
```