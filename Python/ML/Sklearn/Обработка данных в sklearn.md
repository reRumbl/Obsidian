В [[Sklearn|sklearn]] существует множество инструментов для обработки данных.

## Масштабирование данных

Данные масштабируются при помощи специальных [[Классы|классов]] из модуля sklearn.preprocessing, например StandardScaler.

**Пример масштабирования данных:**

```Python
from sklearn import datasets  
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

# Загрузка набора данных
wine = datasets.load_wine()  
X, y = wine.data, wine.target  
  
# Разделение данных  
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=52)
  
# Масштабирование данных  
scaler = StandardScaler()  
X_train_scaled = scaler.fit_transform(X_train)  
X_test_scaled = scaler.transform(X_test)
```