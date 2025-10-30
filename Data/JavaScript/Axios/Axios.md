**Axios** - это [[Cеть/Сетевые протоколы/HTTP/HTTP|HTTP]]-клиент для node.js и браузера.

**Особенности:**

- Делает XmlHttpRequests запросы из браузера.

- Делает Http запросы из node.js.

- Поддерживает Promise API.

**Пример GET запроса при помощи Axios:**

```TypeScript
const axios = require('axios');
const response = await axios.get('/user?ID=12345');
```