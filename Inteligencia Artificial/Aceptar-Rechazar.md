#clase_3 #ag_tag 

# ¿Cómo funcionan los algoritmos de Rejection Sampling?

## **1**. No armamos Mating Pool 

## **2.** Se elige un individuo de los posibles al azar

## **3**.** Paso de “aceptar o rechazar”. Se obtiene un valor aleatorio entre 0 y 1. Si es es menor a la función de aptitud, entonces se acepta. Y sino, se rechaza.

## **4.** Si se acepta, se selecciona el individuo como padre. En cambio, si se rechaza, se vuelve al paso 2. Se itera hasta lograr aceptar algún individuo.


---
# [[Código de Aceptar-Rechazar]]
