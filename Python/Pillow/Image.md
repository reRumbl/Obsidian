[[Классы|Класс]] Image содержится в библиотеке [[Pillow|Pillow]] и позволяет работать с изображениями. Он содержит множество функций и является основным [[Классы|классом]] для библиотеки [[Pillow|Pillow]].

**Импорт класса в проект:**

```Python
from PIL import Image
```

Перед любой работой с изображением его следует открыть из файла или URL.

**Открытие и показ изображения из файла:**

```Python
image = Image.open('Изображения\\Pillow.png')
image.show()
```

Чтобы открыть изображение из URL придется дополнительно использовать встроенную библиотеку [[Requests|requests]], а также конструкции [[Исключения|исключений]].

**Открытие и показ изображения из URL с последующим сохранением:**

```Python
import requests

url = 'https://sportishka.com/uploads/posts/2022-11/1667475216_15-sportishka-com-p-yaponskaya-gora-fudziyama-instagram-16.jpg'

try:
    response = requests.get(url, stream=True).raw
except requests.exceptions.RequestException as e:
    print(e)

try:
    image = Image.open(response)
    image.show()
except IOError:
    print("Unable to open image")

img.save('fujiyama.jpg', 'jpeg')
```

**Информация об изображении через Pillow:**

```Python
image = Image.open('Изображения\\Pillow.png')
r, g, b = image.split()
histogram = image.histogram()
exif = image._getexif(
```

**Обрезка изображения при помощи crop():**

```Python
image = Image.open('Изображения\\Pillow.png')
cropped = image.crop((0, 80, 200, 400))
cropped.save('/path/to/photos/cropped_jelly.png')
```

**Поворот изображения при помощи rotate():**

```Python
image = Image.open('Изображения\\Pillow.png')
rotated = image.rotate(180)
rotated.save('Изображения\\Pillow_rotated.jpg')
```

**Транспозиция изображения при помощи transpose():**

```Python
image = Image.open('Изображения\\Pillow.png')
transposed = image.transpose(Image.Transpose.FLIP_TOP_BOTTOM)
transposed.save('Изображения\\Pillow_rotated.jpg')
```