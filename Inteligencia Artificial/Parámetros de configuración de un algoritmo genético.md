#clas_3 #ag_tag 


## **Consulta interesante realizada a Gemini en base al contenido de la clase**

**Ahora explícame, en que afecta modificar cada uno de estos parámetros?**
--- Parámetros de Configuración del Algoritmo Genético ---
- 🧬 Tamaño de la Población: 100
- 🔄 Número de Generaciones: 500
- ☣️ Tasa de Mutación: 0.02
- 👑 Elitismo (conservar al mejor): Activad

## Output

¡Excelente pregunta! Entender cómo afecta cada parámetro es clave para ajustar y optimizar el algoritmo.

Pensemos en el proceso como si un **grupo de exploradores (la población)** estuviera buscando el **tesoro más valioso (la solución óptima)** en un vasto territorio.

---

### 🧬 **Tamaño de la Población**

Este parámetro define **cuántos exploradores** tienes en tu equipo en cada ronda.

- **Si lo aumentas (ej. de 100 a 500):**
    
    - **Ventaja:** Tienes más exploradores cubriendo más terreno simultáneamente. Aumenta la **diversidad genética**, lo que reduce la probabilidad de que todos se queden atascados en una "colina" pensando que es la montaña más alta (un óptimo local). Hay más "ideas" en juego.
        
    - **Desventaja:** Es computacionalmente más costoso. Cada generación tarda mucho más en calcularse porque tienes que evaluar el desempeño de cada uno de los 500 exploradores.
        
- **Si lo disminuyes (ej. de 100 a 20):**
    
    - **Ventaja:** El algoritmo corre mucho más rápido. Cada generación es liviana y se procesa en un instante.
        
    - **Desventaja:** Con pocos exploradores, es muy fácil que todos terminen siguiendo un camino similar y se convenzan prematuramente de haber encontrado la mejor solución, cuando en realidad podrían haber pasado por alto rutas mucho mejores. Hay un alto riesgo de **convergencia prematura**.
        

**En resumen:** Es un equilibrio entre la **variedad de soluciones** y la **velocidad** del cálculo.

---

### 🔄 **Número de Generaciones**

Este parámetro define **cuánto tiempo (cuántas rondas)** le das a tus exploradores para buscar.

- **Si lo aumentas (ej. de 500 a 2000):**
    
    - **Ventaja:** Les das más tiempo para refinar sus rutas, combinar sus conocimientos (crossover) y tener chispas de nuevas ideas (mutación). Generalmente, a más generaciones, **mejor será la solución final** porque el proceso evolutivo tiene más tiempo para madurar.
        
    - **Desventaja:** El tiempo total de ejecución del algoritmo aumenta linealmente.
        
- **Si lo disminuyes (ej. de 500 a 50):**
    
    - **Ventaja:** Obtienes un resultado muy rápido.
        
    - **Desventaja:** Es muy probable que detengas la búsqueda demasiado pronto. Los exploradores apenas habrán comenzado a encontrar buenos caminos y no tendrán tiempo suficiente para optimizarlos. La solución final probablemente será mediocre.
        

**En resumen:** Es el balance entre la **calidad de la solución** y el **tiempo de espera**.

---

### ☣️ **Tasa de Mutación**

Este parámetro define qué tan a menudo un explorador decide **probar un camino completamente nuevo y aleatorio**. Es la "chispa creativa" del algoritmo.

- **Si la aumentas (ej. de 0.02 a 0.2):**
    
    - **Ventaja:** Se introduce mucha diversidad. Ayuda a que los exploradores no se queden atascados en un mismo valle y los fuerza a explorar lugares inesperados. Es muy útil para **escapar de óptimos locales**.
        
    - **Desventaja:** Si es demasiado alta, el caos reina. Justo cuando un explorador encuentra un camino prometedor, una mutación lo manda a un lugar aleatorio y malo, destruyendo el buen trabajo hecho. Se parece más a una búsqueda aleatoria que a una evolución inteligente.
        
- **Si la disminuyes (ej. de 0.02 a 0.001):**
    
    - **Ventaja:** Permite que las buenas soluciones se refinen y estabilicen. El algoritmo se enfoca en explotar los buenos caminos ya encontrados.
        
    - **Desventaja:** Si es demasiado baja (o cero), el algoritmo pierde su capacidad para introducir nuevas "ideas". Si toda la población comparte rasgos similares, se estancará rápidamente y nunca encontrará soluciones mejores.
        

**En resumen:** Es el equilibrio entre **explorar nuevas posibilidades** y **explotar las soluciones buenas** ya encontradas.

---

### 👑 **Elitismo**

Elitismo significa **proteger al mejor explorador**. Si está activado, el mejor individuo de una generación pasa automáticamente a la siguiente, sin riesgo de ser alterado.

- **Si está activado (como en nuestro caso):**
    
    - **Ventaja:** **Nunca pierdes la mejor solución encontrada hasta el momento**. Asegura que el rendimiento del algoritmo nunca empeore de una generación a la siguiente. Generalmente, acelera la convergencia hacia una buena solución.
        
    - **Desventaja:** Puede contribuir a una ligera reducción de la diversidad, ya que el "mejor" individuo se replica y puede empezar a dominar la población si no hay suficiente mutación.
        
- **Si está desactivado:**
    
    - **Ventaja:** Se mantiene una mayor diversidad genética, ya que todos los individuos de la nueva generación son fruto de la selección y el cruce, sin "favoritos".
        
    - **Desventaja:** Corres el riesgo de que, por mala suerte en la selección o una mutación desafortunada, pierdas al mejor individuo encontrado. Esto puede hacer que el progreso sea más lento e inestable.
        

**En resumen:** Es una estrategia para **asegurar el progreso** a costa de una posible pequeña reducción en la diversidad. En la mayoría de los casos, tenerlo activado es beneficioso.


---

# [[AI - Actividades resueltas (clase 3) - L.E]]
- El algoritmo de la actividad 2 puede ser un buen ejemplo para realizar pruebas: