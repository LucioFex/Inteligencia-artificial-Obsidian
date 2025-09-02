#clase_6
# Ejercicios de Regresión
![[Pasted image 20250901185339.png]]
![[Problemas de Regresión.pdf]]

## Regresión lineal simple
![[Pasted image 20250901185833.png]]
```python
# ===============================
# 1. Importar librerías necesarias
# ===============================
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn import metrics

# ===============================
# 2. Cargar el dataset
# ===============================
# Asegurate de subir el archivo 'used_car_price_vs_mileage.csv' en Colab
df = pd.read_csv("used_car_price_vs_mileage.csv")

# Ver las primeras filas
print(df.head())

# ===============================
# 3. Preparar variables
# ===============================
X = df[["mileage_k_km"]]   # Variable independiente
y = df["price_usd"]        # Variable dependiente

# Dividir en train (70%) y test (30%)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)

# ===============================
# 4. Entrenar el modelo
# ===============================
modelo = LinearRegression()
modelo.fit(X_train, y_train)

# Parámetros de la regresión
print("Intercepto (β0):", modelo.intercept_)
print("Coeficiente (β1):", modelo.coef_[0])

# ===============================
# 5. Evaluación del modelo
# ===============================
y_pred = modelo.predict(X_test)

# Calcular métricas
mae = metrics.mean_absolute_error(y_test, y_pred)
mse = metrics.mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
r2 = metrics.r2_score(y_test, y_pred)

print("\nMétricas de evaluación:")
print(f"MAE (Error Absoluto Medio): {mae:.2f}")
print(f"MSE (Error Cuadrático Medio): {mse:.2f}")
print(f"RMSE (Raíz del Error Cuadrático Medio): {rmse:.2f}")
print(f"R² (Coeficiente de Determinación): {r2:.4f}")

# Explicación de métricas:
# - MAE: error promedio en USD entre predicción y valor real
# - MSE: penaliza más los errores grandes
# - RMSE: error típico esperado en la misma unidad que la variable objetivo (USD)
# - R²: proporción de variabilidad explicada por el modelo (1 = perfecto)

# ===============================
# 6. Graficar scatter y recta ajustada
# ===============================
plt.figure(figsize=(8,6))

# Scatter
sns.scatterplot(data=df, x="mileage_k_km", y="price_usd", label="Datos reales")

# Recta ajustada (genero una grilla ordenada para la línea)
x_line = np.linspace(df["mileage_k_km"].min(), df["mileage_k_km"].max(), 100).reshape(-1, 1)
y_line = modelo.predict(x_line)
plt.plot(x_line.ravel(), y_line, label="Recta ajustada")

plt.xlabel("Kilometraje (miles de km)")
plt.ylabel("Precio (USD)")
plt.title("Regresión lineal simple: Precio vs Kilometraje")
plt.legend()
plt.show()

# ===============================
# 7. Predicciones para valores nuevos
# ===============================
# Ejemplo: autos con 20k, 50k, 120k km
kilometrajes_nuevos = pd.DataFrame({"mileage_k_km":[20, 50, 120]})
predicciones = modelo.predict(kilometrajes_nuevos)

for km, precio in zip(kilometrajes_nuevos["mileage_k_km"], predicciones):
    print(f"Auto con {km*1000:.0f} km -> Precio estimado: {precio:.2f} USD")

```


## Regresión lineal múltiple
![[Pasted image 20250901185845.png]]

## Regresión polinómica (grado 2)
![[Pasted image 20250901185514.png]]

---

Subidos al drive
![[Pasted image 20250901212645.png]]