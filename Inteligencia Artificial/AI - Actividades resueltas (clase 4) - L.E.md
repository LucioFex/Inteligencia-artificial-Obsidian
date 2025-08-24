#clase_4 #ag_tag

# Contenido
```table-of-contents
```

# Actividad
## Actividad (Imagen de la última clase)
![[Pasted image 20250823211006.png]]
## Actividad (Texto)

Recursos:
	Documentación del dataset (incluye CSV): [Data Science Job Salaries 2024](https://www.kaggle.com/datasets/abhinavshaw09/data-science-job-salaries-2024) 

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

1. Cargar el dataset, cambiar el nombre de una columna y modificar, agregar o eliminar al menos una columna
Contesten las siguientes preguntas:  2. 
    a. ¿Hay datos nulos?  
    b. ¿Cuál es el promedio, la moda y la mediana del salario?  
    c. ¿Cuántos trabajos únicos hay? ¿Cuál es el trabajo más usual en compañías L?  
    d. ¿Cuántas personas trabajan para una compañía de su mismo país de residencia?  
    e. ¿Cuántos Data Scientist hay por tamaño de compañía?
3. Piensen una pregunta. Respondan esa pregunta haciendo un análisis en base a al menos 2 columnas de su elección. Utilicen al menos un gráfico y escriban una conclusión sobre su análisis.

# Resolución

## Punto 1: Carga y modificación del dataset
### Actividad solicitada

*Cargar el dataset, cambiar el nombre de una columna y modificar, agregar o eliminar al menos una columna*
### Documentación del dataset:

| Campo                  | Descripción                                                                                                                                                                             |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **work_year**          | The year the salary was paid.                                                                                                                                                           |
| **experience_level**   | The experience level in the job during the year:<br>• EN = Entry-level / Junior<br>• MI = Mid-level / Intermediate<br>• SE = Senior-level / Expert<br>• EX = Executive-level / Director |
| **employment_type**    | The type of employment for the role:<br>• PT = Part-time<br>• FT = Full-time<br>• CT = Contract<br>• FL = Freelance                                                                     |
| **job_title**          | The role worked in during the year.                                                                                                                                                     |
| **salary**             | The total gross salary amount paid.                                                                                                                                                     |
| **salary_currency**    | The currency of the salary paid as an ISO 4217 currency code.                                                                                                                           |
| **salary_in_usd**      | The salary in USD (FX rate divided by avg. USD rate for the respective year via fxdata.foorilla.com).                                                                                   |
| **employee_residence** | Employee's primary country of residence during the work year (ISO 3166 country code).                                                                                                   |
| **remote_ratio**       | The overall amount of work done remotely:<br>• 0 = No remote work (<20%)<br>• 50 = Partially remote<br>• 100 = Fully remote (>80%)                                                      |
| **company_location**   | The country of the employer's main office or contracting branch (ISO 3166 country code).                                                                                                |
| **company_size**       | Average number of employees during the year:<br>• S = <50 (small)<br>• M = 50–250 (medium)<br>• L = >250 (large)                                                                        |
![[Pasted image 20250823213815.png]]
### Archivo de Colab + Outputs: *Clase 4 - Actividad.ipynb*
```python
# Importación de librerías
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Carga del dataset
df_original = pd.read_csv("salaries.csv")
df_modificado = df_original.copy() # Copia superficial (dataset)
```

```python
# Punto 1) *Cargar el dataset, cambiar el nombre de una columna y modificar, agregar o eliminar al menos una columna*

# Cambio del nombre de una columna
df_modificado.rename(columns={'company_location': 'company_country'}, inplace=True)

# Se agrega una nueva columna, y lo que se hace es modificar la conversión del
# salario en euros a partir de un equivalente con USD del 93%.
df_modificado['salary_in_eur'] = df_modificado['salary_in_usd'] * 0.93

# Se eliminan las columnas "salary" y "salary_currency".
df_modificado.drop(['salary', 'salary_currency'], axis=1, inplace=True)

# Visualización de los datos
display(df_original.head())
display(df_modificado.head())
```
![[Pasted image 20250823223648.png]]

## Punto 2: Resolución de preguntas teóricas
Se seguirá utilizando el mismo archivo de Colab + Outputs: *Clase 4 - Actividad.ipynb*.
### Actividad solicitada
*Contesten las siguientes preguntas:  2.* 
    *a. ¿Hay datos nulos?*  
    *b. ¿Cuál es el promedio, la moda y la mediana del salario?*  
    *c. ¿Cuántos trabajos únicos hay? ¿Cuál es el trabajo más usual en compañías L?*  
    *d. ¿Cuántas personas trabajan para una compañía de su mismo país de residencia?*  
    *e. ¿Cuántos Data Scientist hay por tamaño de compañía?*
#### **a.** ¿Hay datos nulos?  
```python
# Punto 2.a) ¿Hay datos nulos?  

print("Cantidad de datos nulos por columna:")
nulos_sumarizados = df_modificado.isnull().sum()
display(nulos_sumarizados)
```
![[Pasted image 20250823234502.png]]
#### **b.** ¿Cuál es el promedio, la moda y la mediana del salario?  
```python
# Punto 2.b) ¿Cuál es el promedio, la moda y la mediana del salario?

# Cálculos + Prints en pantalla (acotados a decimales de dos máx)
salarios_usd = df_modificado['salary_in_usd']
print(f"El promedio del salario en USD es: {salarios_usd.mean():.2f}")
print(f"La mediana del salario en USD es: {salarios_usd.median():.2f}")
print(f"La moda del salario en USD es: {salarios_usd.mode()[0]:.2f}") # El índice [0] es necesario para que la moda no devuelva un type "Series".
```
![[Pasted image 20250823234517 1.png]]
#### **c.** ¿Cuántos trabajos únicos hay? ¿Cuál es el trabajo más usual en compañías L? 
```python
# Punto 2.c) ¿Cuántos trabajos únicos hay? ¿Cuál es el trabajo más usual en compañías L?

# Cantidad de trabajos únicos
print(f"Cantidad de trabajos únicos: {df_modificado['job_title'].nunique()}")

# Trabajo más usual en compañías L
filtro_compañia_l = df_modificado[df_modificado['company_size'] == 'L']['job_title'] # Filtro inicial
trabajo_usual_l = filtro_compañia_l.mode()[0] # Nombre del trabajo más usual
cant_trabajo_usual_l = filtro_compañia_l.value_counts().max() # Cantidad de veces que se repite el trabajo más usual

print(f"El trabajo más usual en compañías 'L' es: {trabajo_usual_l} (cantidad: {cant_trabajo_usual_l})")
```
![[Pasted image 20250823234533.png]]
#### **d.** ¿Cuántas personas trabajan para una compañía de su mismo país de residencia?
```python
# Punto 2.d) ¿Cuántas personas trabajan para una compañía de su mismo país de residencia?

cant_empleados_locales = len(df_modificado[df_modificado['employee_residence'] == df_modificado['company_country']])
print(f"Cantidad de personas que trabajan para una compañía en su mismo país de residencia: {cant_empleados_locales}")
```
![[Pasted image 20250823234549.png]]
#### **e.** ¿Cuántos Data Scientist hay por tamaño de compañía?
```python
# Punto 2.e) ¿Cuántos Data Scientist hay por tamaño de compañía?

# Filtro del dataframe por 'Data Scientist'.
data_scientists_df = df_modificado[df_modificado['job_title'] == 'Data Scientist']

# Agrupación de los datos filtrados, mostrando la cantidad de cada uno.
print("Cantidad de Data Scientist por tamaño de compañía:")
display(data_scientists_df['company_size'].value_counts())
```
![[Pasted image 20250823234605.png]]
## Punto 3: Pregunta teórica + Gráfico
### Actividad
*Piensen una pregunta. Respondan esa pregunta haciendo un análisis en base a al menos 2 columnas de su elección. Utilicen al menos un gráfico y escriban una conclusión sobre su análisis.*
### Pregunta formulada:
**Pregunta: ¿Cuáles son los 10 países de origen de las empresas que ofrecen los salarios más altos?**

### Gráfica de análisis
![[Pasted image 20250824000339.png]]
### Código utilizado en Google Colab
```python
# Punto 3) Piensen una pregunta. Respondan esa pregunta haciendo un análisis en base a al menos 2 columnas de su elección. Utilicen al menos un gráfico y escriban una conclusión sobre su análisis.

# Pregunta: ¿Cuáles son los 10 países de origen de las empresas que ofrecen los salarios más altos?

# 1. Preparar los datos para el gráfico: Agrupar por país de la compañía y calcular el salario promedio en USD.
salario_promedio_por_pais = df_modificado.groupby('company_country')['salary_in_usd'].mean()

# 2. Ordenar los datos de mayor a menor salario promedio.
salario_promedio_por_pais_ordenado = salario_promedio_por_pais.sort_values(ascending=False)

# 3. Crear el gráfico de barras: Generar un gráfico de barras utilizando los datos ordenados.
plt.figure(figsize=(12, 6))

# Definición del colorcamp para la gráfica.
cmap = plt.cm.viridis

# Creación de lista de colores para mostrar en el gráfico de barras.
colores = cmap(np.linspace(0, 1, len(salario_promedio_por_pais_ordenado.head(10))))

salario_promedio_por_pais_ordenado.head(10).plot(kind='bar', color=colores)

# 4. Personalización adicional al gráfico.
plt.title('Top 10 Países con Mayor Promedio de Salario en USD')
plt.xlabel('País de la Compañía')
plt.ylabel('Promedio de Salario en USD')
plt.xticks(rotation=90)
plt.tight_layout()
plt.show()
```