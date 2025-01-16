В [[React|React]] центральная концепция — это **компоненты**. **Компоненты** - это основные строительные блоки для создания пользовательских интерфейсов в [[React|React]]. Они позволяют разбивать интерфейс на независимые, переиспользуемые части, которые можно разрабатывать, тестировать и поддерживать отдельно.

## Основные концепции

- Пропсы (Props): Передаются компоненту сверху вниз и нельзя изменять внутри компонента.

- Состояние (State): Позволяет компонентам хранить и менять данные во время выполнения [1](https://ru.legacy.reactjs.org/docs/components-and-props.html).

- Жизненный цикл компонента: Методы, вызываемые в разных этапах жизни компонента (монтирование, обновление, размонтирование) [5](https://ru.legacy.reactjs.org/docs/react-component.html).

## Типы компонентов
### Функциональные компоненты

Это самые простые компоненты, определяемые как обычные [[JavaScript|JavaScript]]-функции.

**Пример функциональных компонентов:**

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

### Классовые компоненты

Определяются путем расширения [[React|React]].Component.

Пример классового компонента:

```JavaScript
class Welcome extends React.Component {
	render() {
		return <h1>Привет, {this.props.name}</h1>;
	}
}

```


