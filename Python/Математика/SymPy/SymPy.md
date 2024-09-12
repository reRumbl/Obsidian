**SymPy** — это библиотека для символьных вычислений на [[Python|Python]]. Она позволяет работать с математическими выражениями в аналитическом виде, решать уравнения, упрощать выражения и многое другое.

![[SymPy.png]]

**Установка через cmd или terminal:**

```Shell
pip install sympy
```

**Подключение в проект:**

```Python
import sympy
```

## Основы SymPy

**Создание символов**: В SymPy символы объявляются с помощью `symbols()`. Здесь `x` — это переменная, с которой можно работать, как с математическим символом.

**Создание символов при помощи SymPy:**

```Python
from sympy import symbols

x = symbols('x')
```

**Определение выражений**: После объявления символов можно создавать выражения.

**Создание выражения при помощи SymPy:**

```Python
expr = x ** 2 + 2 * x + 1
```

*Символьный вариант:*

$$x^2 + 2x + 1$$

**Упрощение выражений:** SymPy может автоматически упрощать выражения с помощью метода `simplify()`.

**Упрощение выражения в SymPy:**

```Python
simplified_expr = expr.simplify()
```

**Вычисление производных:** **SymPy** может вычислять производную заданного выражения по определенной переменной при помощи функции `diff()`.ч

**Вычисление производной в SymPy:**

```Python
from sympy import diff

derivative = diff(expr, x)
```

## Построение графиков

**Преобразование выражений SymPy в числовые функции**: **SymPy** позволяет преобразовывать символические выражения в числовые функции с помощью метода `lambdify()`. Это удобно для создания графиков в [[Matplotlib|Matplotlib]], так как [[Matplotlib|Matplotlib]] работает с числовыми данными.

**Пример комбинации SymPy и Matplolib:**

```Python
from sympy import symbols, lambdify
import numpy as np 
import matplotlib.pyplot as plt 

# Определяем символы и выражение 
x = symbols('x') 
expr = x**2 + 2*x + 1 

# Преобразуем выражение в функцию для вычисления чисел
f_numeric = lambdify(x, expr, 'numpy') 

# Создаем массив числовых значений для x 
x_vals = np.linspace(-10, 10, 100) 

# Вычисляем значения функции для этих x 
y_vals = f_numeric(x_vals) 

# Строим график 
plt.plot(x_vals, y_vals) 
plt.title('График функции, полученной из SymPy') 
plt.xlabel('x') plt.ylabel('f(x)') 
plt.grid(True) 
plt.show()
```

**Построение графиков производных**: Можно найти производные с помощью **SymPy**, а затем также использовать их для визуализации в [[Matplotlib|Matplotlib]].

**Построение графика производной с SymPy:**

```Python
# Производная от выражения
derivative_expr = expr.diff(x)

# Преобразуем производную в числовую функцию 
f_derivative_numeric = lambdify(x, derivative_expr, 'numpy')

# Вычисляем значения производной 
y_derivative_vals = f_derivative_numeric(x_vals)

# Строим графики 
plt.plot(x_vals, y_vals, label='f(x)') 
plt.plot(x_vals, y_derivative_vals, label="f'(x)", linestyle='--') 
plt.legend() 
plt.grid(True) 
plt.show()
```