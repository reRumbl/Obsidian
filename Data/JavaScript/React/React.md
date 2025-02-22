**React** - это библиотека на [[JavaScript|JavaScript]] с открытым исходным кодом для разработки пользовательских интерфейсов. Её создали разработчики Facebook.

![[React.png]]

**Установка:**

```Shell
npm install react react-dom
```

**Установка необходимых инструментов разработки:**

```Shell
npm install --save-dev webpack webpack-cli webpack-dev-server babel-loader @babel/core @babel/preset-env @babel/preset-react html-webpack-plugin
```
## Создание проекта

Для начала нужно установить `create-react-app`, если он не установлен, чтобы создать новый проект:

```Shell
npx create-react-app my-app --template typescript
```

Это создаст структуру файлов, настроит Webpack и Babel, и позволит быстро начать разработку.

Затем нужно перейти в созданную папку:

```Shell
cd my-app
```

После чего запустить проект:

```Shell
npm start
```

Откроется окно браузера с надписью "Hello, world!" — это и есть стартовый шаблон React.
