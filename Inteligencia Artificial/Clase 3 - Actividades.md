#clase_3 **Alumno**: Luciano Esteban

# Actividad 1
## Consigna
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
Este caso de uso se inspira en el videojuego "Creatures" de 1996 de parte de Steve Grand. El objetivo del juego es criar y enseñarle a criaturas virtuales llamadas "Norns" a sobrevivir en un ecosistema complejo. Para esto se utilizan una serie de algoritmos genéticos altamente complejos (adjuntos junto a los papers oficiales del autor en la sección "*Contenido adicional o de referencia sobre Creatures (1996)*"). Dado que el ejercicio solicitado no precisa ser tan complejo ni extenso, realizaré un algoritmo genétic con pseudo código para evolucionar los comportamientos de los norns, permitiéndoles aprender de forma auónoma a encontrar comida y evitar peligros.

*Imagen de un Norn.*
![[Pasted image 20250816210209.png | 300]]
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
```bash
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




~~**Descripción del ADN: fenotipo y genotipo**~~
**Algoritmo de la función de aptitud (pseudocódigo explicado)**
**Algoritmo de Selección (pseudocódigo explicado)**
**Algoritmo de Crossover (pseudocuódigo explicado)**
**Algoritmo de Mutación (pseudocódigo explicado)**
**Parámetros a utilizar (tamaño de población, factor de mutación, etc.)**
**Condición de final**
**Composición de la población inicial**
**Y todo aquello que considere necesario para explicar cómo resolverá el**
**problema mediante AG.**

**Contenido adicional o de referencia sobre Creatures (1996)**

# Actividad 2
## Consigna
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

