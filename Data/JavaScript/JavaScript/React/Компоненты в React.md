В [[React|React]] центральная концепция — это **компоненты**. **Компоненты** — это маленькие части интерфейса, которые можно переиспользовать и комбинировать, создавая сложные интерфейсы.

## Функциональные компоненты

Компонент в [[React|React]] можно создать с помощью функции. Функциональные компоненты принимают **пропсы** и возвращают JSX (похожий на HTML) для отображения в интерфейсе.

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




