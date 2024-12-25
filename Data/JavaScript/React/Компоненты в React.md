В [[React|React]] центральная концепция — это **компоненты**. **Компоненты** - это основные строительные блоки для создания пользовательских интерфейсов в [[React|React]]. Они позволяют разбивать интерфейс на независимые, переиспользуемые части, которые можно разрабатывать, тестировать и поддерживать отдельно.

## Типы компонентов
### Функциональные компоненты

Компонент в [[React|React]] можно создать с помощью функции. Это самые простые компоненты, определяемые как обычные [[JavaScript|JavaScript]]-функции. Функциональные компоненты принимают **пропсы** и возвращают JSX (похожий на HTML) для отображения в интерфейсе.

**Пример функционального компонента:**

```JavaScript
// Welcome.js
import React from 'react';

function Welcome(props) {
    return <h1>Привет, {props.name}!</h1>;
}

export default Welcome;
```

```JavaScript
// App.js
import React from 'react';
import Welcome from './Welcome';

function App() {
    return (
        <div>
            <Welcome name="Dmitry" />
        </div>
    );
}

export default App;
```




