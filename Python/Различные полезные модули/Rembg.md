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
import numpy as np

image = Image.open('Image with background.png').convert("RGBA")


```

*Результат:*

![[Image without background.png]]