#clase_2 #ag_tag 
# Entrecruzamiento en Algoritmos Evolutivos

## 1) Concepto de Entrecruzamiento
El entrecruzamiento es un operador genético utilizado en algoritmos evolutivos para generar nuevas soluciones a partir de soluciones existentes. Consiste en tomar dos elementos (individuos) con buenas funciones de aptitud y combinarlos para crear uno o más nuevos elementos.
## 2) Ejemplo de Entrecruzamiento
Un ejemplo sencillo de entrecruzamiento sería: Tomar un elemento, cortarlo por la mitad, y luego tomar la primera mitad del primer elemento y la segunda mitad del segundo elemento para crear un nuevo elemento. Esto da una alta probabilidad de que el hijo tenga una mejor función de aptitud que los padres.
## 3) Otras Formas de Entrecruzamiento
Existen otras formas de realizar el entrecruzamiento, como elegir un punto medio al azar, alternar caracteres entre los padres, o asignar 50% de chances a cada carácter. La elección del método depende de la simplicidad y la facilidad de implementación.

---
## Adicional:
- #### El entrecruzamiento comienza en la función generate
- #### Lo primero que se hace es seleccionar al azar los padres del mating pool
- #### Esta función toma la mitad de los DNA del primer padre y la segunda mitad del segundo padre
- #### Con ambos padres, se arma un nuevo individuo en la función crossover

![[Pasted image 20250804212317.png | 200]]

