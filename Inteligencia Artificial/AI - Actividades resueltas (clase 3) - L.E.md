#clase_3 #ag_tag 
**Alumno**: Luciano Esteban
# Actividad 1
Diseñar un caso de uso que se pueda resolver mediante AG, detallando como
mínimo los siguientes puntos:
- Explicación detallada del caso de uso
- Descripción del ADN: fenotipo y genotipo
- Algoritmo de la función de aptitud (pseudocódigo explicado)
- Algoritmo de Selección (pseudocódigo explicado)
- Algoritmo de Crossover (pseudocódigo explicado)
- Algoritmo de Mutación (pseudocódigo explicado)
- Parámetros a utilizar (tamaño de población, factor de mutación, etc.)
- Condición de final
- Composición de la población inicial
- Y todo aquello que considere necesario para explicar cómo resolverá el
problema mediante AG.
## Respuesta

#### **Caso de Uso**: Supervivencia de los Norns en "Creatures" (1996)
![[Imagen de WhatsApp 2025-08-16 a las 20.03.42_ab256a5e.jpg]]
Este caso de uso se inspira en el del videojuego "Creatures" de 1996 de parte de Steve Grand (pionero en algoritmos genéticos en el contexto del entretenimiento y avances científicos de los 90s)

El objetivo del juego es criar y enseñarle a criaturas virtuales llamadas "Norns" a sobrevivir en un ecosistema complejo. Para esto se utilizan una serie de algoritmos genéticos altamente complejos (adjuntos junto a los papers oficiales del autor en la sección "*Contenido adicional/referencia sobre Creatures (1996)*").

Dado que el ejercicio solicitado no precisa ser tan complejo ni extenso, realizaré un algoritmo genético con pseudo código para evolucionar los comportamientos de los Norns, permitiéndoles aprender de forma autónoma a encontrar comida y evitar peligros.

![[Pasted image 20250816210209.png | 300]]
*Imagen de un Norn.*
#### **1**. ADN: Genotipo y Fenotipo
Para resolver este problema, vamos a definir la genética de los Norns de esta manera:
- **Genotipo:** Va a ser el código genético que define el comportamiento del Norn. Lo vamos a representar como una serie de genes, donde cada uno va a ser un "vector de fuerza y direccionamiento" que se va a activar bajo determinadas circunstancias (ej: cuando el bichito ve comida).
  Esto sería equivalente a los arrays de caracteres de ejemplo que vimos en clase con "To be or not to be...".
- **Fenotipo:** Esta es la manifestación visible del genotipo. En este caso, va a ser el comportamiento observable del Norn.
	- Cómo se mueve por el mapa.
	- Su velocidad.
	- Las decisiones que toma al interactuar con el entorno.
#### **2**. Algoritmo de la Función de Aptitud
La función de aptitud va a evaluar que tan "exitoso" es un Norn. Un Norn exitoso es aquel que se mantiene bien alimentado y explora eficientemente su entorno.
```python
FUNCIÓN calcular_aptitud(norn):
  puntos_supervivencia = norn.tiempo_de_vida
  puntos_comida = norn.comida_ingerida * 10
  penalización_hambre = norn.tiempo_con_hambre * -5
  
  aptitud_total = puntos_supervivencia + puntos_comida + penalización_hambre
  
  RETORNAR aptitud_total
```

Este algoritmo asigna un puntaje a cada Norn, lo cual es similar a cómo se calculaba la aptitud en el ejemplo de la frase objetivo, pero adaptado a la supervivencia

![[Imagen de WhatsApp 2025-08-16 a las 20.20.38_2f9c21ba.jpg | 400]]
*Captura de ejemplo adaptada del paper de Steve Grand.*
#### **3**. Algoritmo de Selección: Rueda de la Fortuna (Mating Pool)
Para seleccionar a los padres de la siguiente generación, vamos a usar el método de la "Rueda de la Fortuna" visto en clase (Mating Pool).
Los Norns con *mayor aptitud* van a tener más probabilidades de ser elegidos, asegurando que los rasgos exitosos se transmitan.

```python
FUNCIÓN seleccionar_padres(poblacion):
  mating_pool = []
  
  PARA CADA norn EN poblacion:
    aptitud_normalizada = norn.aptitud / aptitud_total_poblacion
    boletos = aptitud_normalizada * 100
    
    REPETIR boletos VECES:
      AÑADIR norn A mating_pool
      
  padre_A = ELEGIR_AL_AZAR(mating_pool)
  padre_B = ELEGIR_AL_AZAR(mating_pool)
  
  RETORNAR padre_A, padre_B
```
Con este método estamos asegurando que los Norns con menor aptitud tengan una posibilidad pequeña de reproducirse, manteniendo la diversidad genética.
#### **4**. Algoritmo de Crossover (Entrecruzamiento)
El crossover combina el ADN de dos padres con el fin de crear un nuevo Norn. Para eso lo que hace es mezclas sus características genéticas.
```python
FUNCIÓN entrecruzar(padre_A, padre_B):
  punto_corte = ELEGIR_AL_AZAR(0, longitud(padre_A.adn))
  
  adn_hijo = SUBSECUENCIA(padre_A.adn, 0, punto_corte) + 
             SUBSECUENCIA(padre_B.adn, punto_corte, fin)
             
  hijo = crear_norn(adn_hijo)
  
  RETORNAR hijo
```
Este proceso (al igual que en el ejemplo de la teoría) toma una parte del ADN de cada progenitor para formar el del descendiente.
#### **5**. Algoritmo de Mutación
La mutación en este caso introduce cambios que son aleatorios en el ADN del nuevo Norn. Esto va a ser clave para la generación de nuevos comportamientos que podrían resultar "ventajosos".
```python
FUNCIÓN mutar(norn, tasa_mutacion):
  PARA CADA gen EN norn.adn:
    SI ELEGIR_AL_AZAR(0, 1) < tasa_mutacion:
      gen = generar_gen_aleatorio()
      
  RETORNAR norn
```
Una pequeña probabilidad de mutación (ej: 1%) lo que hace es evitar la pérdida de diversidad genética y posibilita la aparición de nueva habilidades (pequeños mutantes podríamos decir).

![[Pasted image 20250816214032.png]]
*Imagen de múltiples tipos de Norn.*
#### **6**. Parámetros y Composición de la Población
- **Población inicial**: Se va a crear una población de Norns con ADN completamente aleatorio.
- **Tamaño de la población:** Un número moderado, como 100 Norns, podría ser suficiente para tener tener variedad sin sobrecargar la simulación.
- **Tasa de mutación**: Se va a fijar en un 1% para fomentar la exploración de nuevas soluciones sin desestabilizar los rasgos que ya fueron probados como exitosos.
- **Condición de final**: El algoritmo se va a detener tras un número determinado de generaciones (ej: 500) o cuando la aptitud promedio de la población se estabilice, indicando uqe se ha encontrado una solución óptima.
- **Reemplazo:** La población original va a ser completamente reemplazada por la nueva generación en cada ciclo.

Ya con esto, el AG (algoritmo genético) va a simular la evolución darwiniana, donde los Norns más aptos para encontrar comida sobrevivirán y se reproducirán, mejorando gradualmente las habilidades de la población a lo largo de las generaciones.

#### **Adicional: 7**. Contenido adicional/referencia sobre Creatures (1996)

![[Imagen de WhatsApp 2025-08-16 a las 20.07.06_a63a33a7.jpg | 400]]
*Genetics Kit de configuración manual de Norns.*

![[Imagen de WhatsApp 2025-08-16 a las 20.21.43_84f88cae.jpg |500]]
*Acciones y elementos vinculados a los Norns.*

![[Imagen de WhatsApp 2025-08-16 a las 20.27.02_4aa70f72.jpg | 400]]
*Paper 1 - Creatures: Artificial Life Autonomous Software Agents for Home Entertainment:* https://svn.sable.mcgill.ca/sable/courses/COMP763/oldpapers/grand-97-creatures.pdf

![[Pasted image 20250816220019.png | 400]]
*Paper 2 - Creatures: Entertainment Software Agents with Artificial Life:* https://www.researchgate.net/publication/226997131_Creatures_Entertainment_Software_Agents_with_Artificial_Lifef

*Blog y video resumen de Alan Zucconi:*
- Blog: https://www.alanzucconi.com/2020/07/27/the-ai-of-creatures/
- Video: https://www.youtube.com/watch?v=Y-6DzI-krUQ&ab_channel=AlanZucconi

# Actividad 2
Estamos ante el caso de una empresa que está abriendo 2 nuevas oficinas.
En la primera, en Saveedra, cuenta con 5 espacios y en la segunda, en Pilar,
cuenta con 8 espacios. La empresa debe asignar cada uno de los 13 espacios
a las distintas áreas de trabajo (marketing, contabilidad, data, ventas, RRHH,
finanzas, operaciones, etc).
Decide asignar los espacios teniendo en cuenta dos factores principales:
- La distancia entre los espacios
- El flow de personas que se van y se comunican de un área a la otra
durante el día.
El objetivo es minimizar la distancia total recorrida por los empleados de la
empresa para garantizar una mayor productividad.
Para tomar esa decisión utilizaremos un algoritmo genético. Este es un
problema de optimización.
## Respuesta

#### Script de Python para Optimización de Espacios de Oficina

Este script utiliza un algoritmo genético para encontrar la asignación óptima de áreas de trabajo en dos oficinas, minimizando la distancia total recorrida por los empleados.

Antes de presentar el script, adjuntaré una matriz de distancias de ejemplo para realizar pruebas consistentes respecto al cambio de parámetros de configuración para esta actividad.
![[Pasted image 20250817011233.png]]

**Script:**
```python
import random
import numpy as np
import pandas as pd

# --- 1. Definición del Problema ---

# Áreas de la empresa
areas = [
    "Marketing", "Contabilidad", "Data", "Ventas", "RRHH",
    "Finanzas", "Operaciones", "Legales", "IT", "Producto",
    "Dirección", "Soporte", "Diseño"
]
n_areas = len(areas)

# --- Matriz de distancias (ESTÁTICA Y REALISTA) ---
# Espacios 0-4 son Saavedra (distancias internas bajas)
# Espacios 5-12 son Pilar (distancias internas bajas)
# Distancia entre Saavedra y Pilar es alta (ej. 1000)

# Creamos una matriz base con la distancia inter-oficina
distancias = np.full((n_areas, n_areas), 1000)

# Asignamos distancias bajas dentro de Saavedra (espacios 0 a 4)
distancias_saavedra = np.array([
    [0, 10, 15, 20, 25],
    [10, 0, 12, 18, 22],
    [15, 12, 0, 10, 15],
    [20, 18, 10, 0, 10],
    [25, 22, 15, 10, 0]
])
distancias[0:5, 0:5] = distancias_saavedra

# Asignamos distancias bajas dentro de Pilar (espacios 5 a 12)
distancias_pilar = np.array([
    [0, 10, 15, 20, 25, 30, 35, 40],
    [10, 0, 10, 15, 20, 25, 30, 35],
    [15, 10, 0, 10, 15, 20, 25, 30],
    [20, 15, 10, 0, 10, 15, 20, 25],
    [25, 20, 15, 10, 0, 10, 15, 20],
    [30, 25, 20, 15, 10, 0, 10, 15],
    [35, 30, 25, 20, 15, 10, 0, 10],
    [40, 35, 30, 25, 20, 15, 10, 0]
])
distancias[5:13, 5:13] = distancias_pilar

# Matriz de flow de comunicación (ESTÁTICA)
flow = np.array([
    [0, 47, 0, 3, 3, 39, 9, 19, 21, 36, 23, 6, 24],
    [24, 0, 1, 38, 39, 23, 46, 24, 17, 37, 25, 13, 8],
    [9, 20, 0, 5, 15, 47, 0, 18, 35, 24, 49, 29, 19],
    [19, 14, 39, 0, 1, 9, 32, 31, 10, 23, 35, 11, 28],
    [34, 0, 0, 36, 0, 38, 40, 17, 15, 4, 41, 42, 31],
    [1, 1, 39, 41, 35, 0, 11, 46, 18, 27, 0, 14, 35],
    [12, 42, 20, 11, 4, 6, 0, 47, 3, 12, 36, 40, 14],
    [15, 20, 35, 23, 15, 13, 21, 0, 49, 5, 41, 35, 0],
    [31, 5, 30, 0, 49, 36, 34, 48, 0, 3, 34, 42, 13],
    [48, 39, 21, 9, 0, 10, 43, 23, 2, 0, 35, 30, 3],
    [18, 46, 35, 20, 17, 27, 14, 41, 1, 36, 0, 22, 43],
    [40, 11, 2, 16, 32, 0, 38, 19, 46, 42, 40, 0, 30],
    [24, 2, 3, 30, 34, 43, 13, 48, 40, 8, 19, 31, 0]
])


print("\n--- Matriz de Flow de Comunicación entre Áreas (Datos Fijos) ---")
flow_df = pd.DataFrame(flow, index=areas, columns=areas)
print(flow_df)
print("-" * 70)


# --- 2. Parámetros del Algoritmo Genético ---
TAMANO_POBLACION = 100
N_GENERACIONES = 500
TASA_MUTACION = 0.02
ELITISMO = True

# --- Impresión de Parámetros de Configuración ---
print("\n--- Parámetros de Configuración del Algoritmo Genético ---")
print(f"1. Tamaño de la Población: {TAMANO_POBLACION}")
print(f"2. Número de Generaciones: {N_GENERACIONES}")
print(f"3. Tasa de Mutación: {TASA_MUTACION}")
print(f"4. Elitismo (conservar al mejor): {'Activado' if ELITISMO else 'Desactivado'}")
print("-" * 70)


# --- 3. Componentes del Algoritmo Genético ---
def crear_individuo():
    return random.sample(areas, n_areas)

def crear_poblacion_inicial():
    return [crear_individuo() for _ in range(TAMANO_POBLACION)]

def calcular_costo(individuo):
    costo_total = 0
    for i in range(n_areas):
        for j in range(n_areas):
            area1 = individuo[i]
            area2 = individuo[j]
            idx1 = areas.index(area1)
            idx2 = areas.index(area2)
            distancia_entre_espacios = distancias[i][j]
            flow_entre_areas = flow[idx1][idx2]
            costo_total += distancia_entre_espacios * flow_entre_areas
    return costo_total

def seleccionar_padres(poblacion_evaluada):
    poblacion_ordenada = sorted(poblacion_evaluada, key=lambda x: x[1])
    mejores_individuos = [ind for ind, costo in poblacion_ordenada[:TAMANO_POBLACION // 2]]
    padre1 = random.choice(mejores_individuos)
    padre2 = random.choice(mejores_individuos)
    return padre1, padre2

def crossover(padre1, padre2):
    hijo = [None] * n_areas
    inicio, fin = sorted(random.sample(range(n_areas), 2))
    hijo[inicio:fin] = padre1[inicio:fin]
    puntero_padre2 = 0
    for i in range(n_areas):
        if hijo[i] is None:
            while padre2[puntero_padre2] in hijo:
                puntero_padre2 += 1
            hijo[i] = padre2[puntero_padre2]
    return hijo

def mutar(individuo):
    if random.random() < TASA_MUTACION:
        idx1, idx2 = random.sample(range(n_areas), 2)
        individuo[idx1], individuo[idx2] = individuo[idx2], individuo[idx1]
    return individuo

# --- 4. Ciclo Evolutivo ---
def ejecutar_algoritmo_genetico():
    print("\n--- Iniciando Proceso de Optimización Genética ---")
    poblacion = crear_poblacion_inicial()

    for generacion in range(N_GENERACIONES):
        poblacion_evaluada = [(ind, calcular_costo(ind)) for ind in poblacion]
        nueva_poblacion = []
        if ELITISMO:
            mejor_individuo = sorted(poblacion_evaluada, key=lambda x: x[1])[0][0]
            nueva_poblacion.append(mejor_individuo)
        while len(nueva_poblacion) < TAMANO_POBLACION:
            padre1, padre2 = seleccionar_padres(poblacion_evaluada)
            hijo = crossover(padre1, padre2)
            hijo_mutado = mutar(hijo)
            nueva_poblacion.append(hijo_mutado)
        poblacion = nueva_poblacion
        if (generacion + 1) % 100 == 0:
            mejor_costo = min([costo for ind, costo in poblacion_evaluada])
            print(f"Generación {generacion + 1}: Mejor costo = {mejor_costo}")

    # --- 5. Resultado Final ---
    poblacion_final_evaluada = [(ind, calcular_costo(ind)) for ind in poblacion]
    mejor_solucion, mejor_costo_final = sorted(poblacion_final_evaluada, key=lambda x: x[1])[0]

    print("\n--- Mejor Asignación Encontrada ---")
    print(f"Costo Total Mínimo: {mejor_costo_final}")
    print("\nDistribución:")
    print("A. Oficina Saavedra (Espacios 0-4):")
    for i in range(5):
        print(f"  Espacio {i}: {mejor_solucion[i]}")

    print("\nB. Oficina Pilar (Espacios 5-12):")
    for i in range(5, 13):
        print(f"  Espacio {i}: {mejor_solucion[i]}")

# Ejecutar el algoritmo
ejecutar_algoritmo_genetico()
```
#### Pruebas con múltiples variaciones en los parámetros de configuración

##### Prueba 1
```python
--- Parámetros de Configuración del Algoritmo Genético ---
1. Tamaño de la Población: 100
2. Número de Generaciones: 500
3. Tasa de Mutación: 0.02
4. Elitismo (conservar al mejor): Activado
----------------------------------------------------------------------

--- Iniciando Proceso de Optimización Genética ---
Generación 100: Mejor costo = 1547843
Generación 200: Mejor costo = 1547843
Generación 300: Mejor costo = 1547843
Generación 400: Mejor costo = 1547843
Generación 500: Mejor costo = 1547843

--- Mejor Asignación Encontrada ---
Costo Total Mínimo: 1547843

Distribución:
A. Oficina Saavedra (Espacios 0-4):
  Espacio 0: Ventas
  Espacio 1: Operaciones
  Espacio 2: Contabilidad
  Espacio 3: Producto
  Espacio 4: Marketing

B. Oficina Pilar (Espacios 5-12):
  Espacio 5: RRHH
  Espacio 6: Finanzas
  Espacio 7: Diseño
  Espacio 8: Soporte
  Espacio 9: IT
  Espacio 10: Legales
  Espacio 11: Dirección
  Espacio 12: Data
```
##### Prueba 2
```python
--- Parámetros de Configuración del Algoritmo Genético ---
1. Tamaño de la Población: 400
2. Número de Generaciones: 500
3. Tasa de Mutación: 0.02
4. Elitismo (conservar al mejor): Activado
----------------------------------------------------------------------

--- Iniciando Proceso de Optimización Genética ---
Generación 100: Mejor costo = 1548694
Generación 200: Mejor costo = 1548694
Generación 300: Mejor costo = 1548694
Generación 400: Mejor costo = 1548581
Generación 500: Mejor costo = 1548581

--- Mejor Asignación Encontrada ---
Costo Total Mínimo: 1548581

Distribución:
A. Oficina Saavedra (Espacios 0-4):
  Espacio 0: Marketing
  Espacio 1: Producto
  Espacio 2: Contabilidad
  Espacio 3: Operaciones
  Espacio 4: Ventas

B. Oficina Pilar (Espacios 5-12):
  Espacio 5: Data
  Espacio 6: Finanzas
  Espacio 7: Diseño
  Espacio 8: RRHH
  Espacio 9: Dirección
  Espacio 10: IT
  Espacio 11: Legales
  Espacio 12: Soporte
```
##### Prueba 3
```python
--- Parámetros de Configuración del Algoritmo Genético ---
1. Tamaño de la Población: 250
2. Número de Generaciones: 800
3. Tasa de Mutación: 0.06
4. Elitismo (conservar al mejor): Activado
----------------------------------------------------------------------

--- Iniciando Proceso de Optimización Genética ---
Generación 100: Mejor costo = 1547783
Generación 200: Mejor costo = 1547783
Generación 300: Mejor costo = 1547783
Generación 400: Mejor costo = 1547783
Generación 500: Mejor costo = 1547783
Generación 600: Mejor costo = 1547783
Generación 700: Mejor costo = 1547783
Generación 800: Mejor costo = 1547783

--- Mejor Asignación Encontrada ---
Costo Total Mínimo: 1547783

Distribución:
A. Oficina Saavedra (Espacios 0-4):
  Espacio 0: Ventas
  Espacio 1: Operaciones
  Espacio 2: Contabilidad
  Espacio 3: Producto
  Espacio 4: Marketing

B. Oficina Pilar (Espacios 5-12):
  Espacio 5: Data
  Espacio 6: Finanzas
  Espacio 7: Dirección
  Espacio 8: Legales
  Espacio 9: IT
  Espacio 10: Diseño
  Espacio 11: Soporte
  Espacio 12: RRHH
```
##### Prueba 4
```python
--- Parámetros de Configuración del Algoritmo Genético ---
1. Tamaño de la Población: 1500
2. Número de Generaciones: 400
3. Tasa de Mutación: 0.03
4. Elitismo (conservar al mejor): Activado
----------------------------------------------------------------------

--- Iniciando Proceso de Optimización Genética ---
Generación 100: Mejor costo = 1547781
Generación 200: Mejor costo = 1547781
Generación 300: Mejor costo = 1547781
Generación 400: Mejor costo = 1547781

--- Mejor Asignación Encontrada ---
Costo Total Mínimo: 1547781

Distribución:
A. Oficina Saavedra (Espacios 0-4):
  Espacio 0: Marketing
  Espacio 1: Producto
  Espacio 2: Contabilidad
  Espacio 3: Operaciones
  Espacio 4: Ventas

B. Oficina Pilar (Espacios 5-12):
  Espacio 5: RRHH
  Espacio 6: Soporte
  Espacio 7: Diseño
  Espacio 8: IT
  Espacio 9: Legales
  Espacio 10: Dirección
  Espacio 11: Finanzas
  Espacio 12: Data
```
