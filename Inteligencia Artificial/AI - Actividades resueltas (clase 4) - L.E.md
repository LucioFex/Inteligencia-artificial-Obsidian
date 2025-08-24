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
2. Contesten las siguientes preguntas:  
    a. ¿Hay datos nulos?  
    b. ¿Cuál es el promedio, la moda y la mediana del salario?  
    c. ¿Cuántos trabajos únicos hay? ¿Cuál es el trabajo más usual en compañías L?  
    d. ¿Cuántas personas trabajan para una compañía de su mismo país de residencia?  
    e. ¿Cuántos Data Scientist hay por tamaño de compañía?
3. Piensen una pregunta. Respondan esa pregunta haciendo un análisis en base a al menos 2 columnas de su elección. Utilicen al menos un gráfico y escriban una conclusión sobre su análisis.

# Resolución

# Punto 1: Carga y modificación del dataset

### Documentación del dataset:

| Campo              | Descripción                                                                                                                                                                             |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
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

### Archivo de Colab: *Clase 4 - Actividad.ipynb*
```python

```

## Punto 2: Resolución de preguntas teóricas
Lorem ipsum
## Punto 3: Pregunta teórica adicional + Gráfico
Lorem ipsum

