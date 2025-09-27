[[MaterialUI|MatetialUI]] предоставляет обширный список компонентов, использовать которые можно просто импортировав их из библиотеки.

**Пример использования компонента Button:**

```TypeScript
import * as React from 'react';
import Button from '@mui/material/Button';


export default function ButtonContained() {
	return <Button variant='contained'>Hello world</Button>;
}


export function ButtonOutline() {
	return <Button variant='outlined'>Hello world</Button>;
}
```