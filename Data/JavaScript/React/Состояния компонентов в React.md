**Состояние** - это внутренние данные [[Компоненты в React|компонента]] [[React|React]], которые могут меняться во время выполнения приложения. Оно определяется в конструкторе компонента и используется для управления состоянием UI.

**Основные свойства:**

- **Состояние** - это объект, который хранится внутри компонента.

- Его можно изменять только через `setState`, прямое изменение запрещено.

- Состояние обновляется асинхронно, новые значения доступны только после следующего рендеринга.

- Используется для управления интерактивностью компонента и его внешнего вида.

## Состояния в классовых компонентах

Для управления состоянием в классовом [[Компоненты в React|компоненте]] требуется ввести специальную переменную `state` типа `object` в конструкторе. В нее можно занести все динамические свойства. Изменять свойства можно при помощи `this.setState`, а обращаться при помощи `this.state`.

**Пример классового компонента с состоянием:**

```TypeScript
import React from 'react';


interface ICounterProps {
    initialValue?: number;
}


interface ICounterState {
    count: number;
}


export default class Counter extends React.Component<ICounterProps, ICounterState> {
    constructor(props: ICounterProps) {
        super(props);
        this.state = {
            count: props.initialValue || 0,
        };
    }

    increment = () => {
        this.setState({ count: this.state.count + 1 });
    };

    decrement = () => {
        this.setState({ count: this.state.count - 1 });
    };

    render() {
        return (
            <div>
                <p>Текущее значение: {this.state.count}</p>
                <button onClick={this.increment}>Увеличить</button>
                <button onClick={this.decrement}>Уменьшить</button>
            </div>
        );
    }
}
```