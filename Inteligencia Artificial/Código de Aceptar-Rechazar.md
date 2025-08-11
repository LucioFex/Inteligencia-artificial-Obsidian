#clase_3 #ag_tag 

# VAMOS AL CODIGO DE Aceptar/Rechazar

## **1.** Eliminamos la función naturalSelection
Ya no se necesita armar el mating pool. (<mark style="background: #FFF3A3A6;">Ojo con la foto, no sé bien si va en esta sección</mark>)
![[Pasted image 20250811190737.png | 600]]
## **2.** Reemplazamos la selección de los padres
En la función generate() de Population.js
![[Pasted image 20250811192014.png]]
## **3.** Sumamos 1% a la aptitud del individuo
Para evitar que el algoritmo colapse si todas las frases tienen 0 coincidencias
## 4. Creamos un array para la nueva generación
Para evitar pisar individuos de la generación actual. Esto no sucedía en el algoritmo anterior pues los individuos se elegían del Mating Pool
## 5. Modificamos el final del algoritmo cambiando el ">" por ">="
Debido al incremento artificial de 1% a la función de aptitud


---

### Ejemplo de un algoritmo durante la clase

![[Pasted image 20250811192414.png]]
- Este es un ejemplo de un algoritmo genético que va más rápido, porque se evita la creación del Mating Pool.
