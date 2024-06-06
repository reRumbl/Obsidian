**Rembg** - модуль, который позволяет удалять задний фон с изображений.

![[Rembg.png]]

**Установка через cmd или terminal:**

```Python
pip install rembg
```

**Подключение в проект:**

```Python
import rembg
```

Удаление заднего фона осуществляется при помощи функции **remove**, она может принимать в себя данные в формате байтов, изображений [[Image|Pillow Image]], а также массивов [[Array|NumPy Array]].

**Пример использования функции remove:**

*Входное изображение:*

![[Image with background.png]]

*Код:*

```Python
from PIL import Image

image = Image.open('Image with background.png').convert("RGBA")
image_rembg = rembg.remove(image)
image_rembg.save('Image without background.png')
```

*Результат:*

![[Image without background.png]]

**Получение маски объекта при помощи функции remove:**

```Python
from PIL import Image
import numpy as np

image = Image.open('Image with background.png').convert("RGBA")
np_image = np.array(image)
mask = remove(np_image, only_mask=True)
```