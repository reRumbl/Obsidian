**Scikit-Learn** — это библиотека машинного обучения на языке [[Python|Python]], которая предоставляет простые и эффективные инструменты для анализа и моделирования данных. Она включает в себя множество алгоритмов для классификации, регрессии, кластеризации и снижения размерности.

![[Scikit Learn.png]]

**Основные концепции:**

- **Datasets**: **Scikit-Learn** содержит встроенные наборы данных для обучения и тестирования.

- **Estimators**: Объекты, которые могут обучаться на данных. Все алгоритмы машинного обучения представлены в виде эстиматоров.

- **Transformers**: Объекты, которые могут преобразовывать данные. Обычно применяются для предварительной обработки данных.

- **Pipelines**: Позволяют объединить несколько шагов обработки и моделирования данных в единый процесс.

**Установка через cmd или terminal:**

```Python
pip install scikit-learn
```

**Подключение в проект:**

```Python
import sklearn
```

**Пример кода обучения с использованием sklearn:**

```Python
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score

# Загрузка данных
iris = datasets.load_iris()
X, y = iris.data, iris.target

# Разделение данных
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Инициализация модели
knn = KNeighborsClassifier(n_neighbors=3)

# Обучение модели
knn.fit(X_train, y_train)

# Предсказания на тестовых данных
y_pred = knn.predict(X_test)

# Оценка точности модели
accuracy = accuracy_score(y_test, y_pred)
print(f"Accuracy: {accuracy:.2f}")
```
