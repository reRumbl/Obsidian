**ReactRouterDOM** - это библиотека для [[React|React]], которая позволяет удобно организовывать навигацию между страницами.

**Установка:**

```Shell
npm install react react-dom
```

## Роутинг при помощи ReactRouterDOM

Чтобы организовать роутинг используются специальные компоненты `<Router>`, `<Routes>` и `<Route>` из `BrowserRouter`.

**Пример роутинга при помощи ReactRouterDOM:**

```TypeScript
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Home from './pages/Home.tsx';
import Login from './pages/Login.tsx';
import ProductList from './pages/ProductList.tsx';


const App: React.FC = () => {
    return (
        <Router>
            <Routes>
                <Route path='/' element={<Home />} />
                <Route path='/login' element={<Login />} />
                <Route path='/products' element={<ProductList />} />
            </Routes>
        </Router>
    );
};


export default App;
```