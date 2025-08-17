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
*Imagen con múltiples tipos de Norn.*
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

