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

**Пример кода обучения на разных моделях с использованием sklearn:**

```Python
from sklearn import datasets  
from sklearn.model_selection import train_test_split  
from sklearn.neighbors import KNeighborsClassifier  
from sklearn.metrics import accuracy_score  
from sklearn.preprocessing import StandardScaler  
from sklearn.linear_model import LogisticRegression  
from sklearn.svm import SVC  
  
# Загрузка данных  
wine = datasets.load_wine()  
X, y = wine.data, wine.target  

# Разделение данных  
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=52)  

# Масштабирование данных  
scaler = StandardScaler()  
X_train_scaled = scaler.fit_transform(X_train)  
X_test_scaled = scaler.transform(X_test)  

# KNN  
knn = KNeighborsClassifier(n_neighbors=10)  
knn.fit(X_train_scaled, y_train)  

y_pred = knn.predict(X_test_scaled)  

accuracy = accuracy_score(y_test, y_pred)  
print(f"Accuracy of KNN: {accuracy:.2f}")  

# LR  
log_reg = LogisticRegression(max_iter=1000)  
log_reg.fit(X_train_scaled, y_train)  

y_pred = log_reg.predict(X_test_scaled)  

accuracy_log_reg = accuracy_score(y_test, y_pred)  
print(f"Accuracy of Logistic Regression: {accuracy_log_reg:.2f}")  

# SVM  
svm = SVC()  
svm.fit(X_train_scaled, y_train)  

y_pred = svm.predict(X_test_scaled)  

accuracy_svm = accuracy_score(y_test, y_pred)  
print(f"Accuracy of SVM: {accuracy_svm:.2f}")
```
