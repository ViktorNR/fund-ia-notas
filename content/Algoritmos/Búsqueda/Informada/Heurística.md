En Inteligencia Artificial, una heurística es una **estrategia** o **método práctico** que se utiliza para resolver problemas o tomar decisiones de manera más rápida y eficiente, especialmente cuando no es factible encontrar una solución óptima en un tiempo razonable.

**Definición:** Una heurística es una **regla empírica** o atajo que guía la [[Algoritmo de Búsqueda|búsqueda]] de soluciones, sacrificando en algunos casos la exactitud por la eficiencia.

**Características prinicipales:**
- **No garantiza la mejor solución**, pero suele encontrar una solución *suficientemente buena*.
- Es útil en **problemas complejos o con espacios de búsqueda muy grandes**.
---

### Heurísitca Manhattan
Es una heurística que calcula la **distancia entre dos puntos** como si solo pudieras moverte en **líneas rectas horizontales o verticales**.

**Formula**
Para dos puntos en una cuadrícula:
$$h(n) = |x_1 - x_2| + |y_1 - y_2|$$
Donde:
- $(x_1, y_1)$: posición actual (nodo).
- $(x_2, y_2)$: posición objetivo.

**Usos comunes**
- Juegos como laberintos.
- Algoritmos de búsqueda como [[AStar (A estrella o A asterísco)|A*]] en mapas de robots o videojuegos.
- Problemas de rutas o planificación urbana.

**Ventajas**
- **Simple y rápida de calcular**.
- Es adminisible (no sobrestima el costo real) si el movimiento diagonal no está permitido.
---
### Heurística Euclidiana
La heurística euclidiana es la medida directa *en línea recta* entre dos puntos en un espacio. Viene de la geometría clásica y es la misma formula que se usa para medir distancias en un plano.

**Formula**
Para dos puntos en una cuadrícula:
$$h(n) = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}$$
Donde:
- $(x_1, y_1)$: posición actual (nodo).
- $(x_2, y_2)$: posición objetivo.

**Usos comunes**
- En mapas donde el agente puede moverse **en cualquier dirección**, no solo vertical/horizontal.
- En algoritmos como [[AStar (A estrella o A asterísco)|A*]] cuando el entorno **permite diagonales**.

**Ventajas**
- Más precisa que la heurística Manhattan cuando el movimiento no está restringido a una cuadrícula.
- Admisible (si no se sobrestima) y consistente.
---
### Heurística MRV
Por sus siglas en ingles *Minimum Remaining Values* (Valores Mínimos Restantes), esta heurística elige **primero la variable con menos valores posibles restantes en su dominio** (es decir, la variable **más restringida** en ese momento).

**¿Por qué usar MRV**
La idea es **detectar pronto los conflictos:**
Si una variable tiene **muy pocas opciones disponibles**, es más probable que cause un **fallo de consistencia** si no se maneja de inmediato.
> Elegirla primero permite **fallar rápido y retroceder antes**, en lugar de seguir explorando soluciones inviables más adelante.

**Ejemplo:**
Supongamos que estamos resolviendo un sudoku, y tenemos tres casillas vacías.
- Casilla A: puede ser $\{1, 2, 3 , 5\}$
- Casilla B: puede ser $\{2, 3\}$
- Casilla C: puede ser $\{1\}$
Con MRV, se elige primero la casilla **C**, porque **solo tiene 1 valor posible**; es la más cercana a generar un conflicto.

**Pseudocódigo**
```
1. Mientras queden variables por asignar:
   a. Selecciona la variable con el menor numero de valores posibles (MRV).
   b. Intenta asignar un valor valido.
   c. Si no hay valores posibles, retrocede (backtrack)
```

**Ventajas**
- Reduce el tamaño del espacio de búsqueda.
- Detecta fallos tempranamente - *fail fast*.
- Efectivo en combinación otras heurísticas como forward checking.

**Desventajas**
- Tiene un costo de calculo adicional, ya que debe evaluar el dominio restante de cada variable **en cada paso**.
- **No decide qué valor usar**; solo qué variable elegir.
---
### Heurística LCV
Por sus siglas en ingles *Least Constraining Value*, es una heurística que elige el valor que **menos restringe las opciones de las damás variables**. Es decir, asigna primero el valor que cause menos problemas futuros.

**¿Por qué usar LCV?**
El objetivo es maximizar la flexibilidad futura del sistema. Al probar primero con valores menos restrictivos, aumenta la probabilidad de que las siguientes variables puedan encontrar valores válidos sin tener que retroceder (backtracking).

**Pseudocódigo**
```
1. Se elige una variable.
2. Mientras queden variables por asignar:
   a. Para cada valor, calcula cuantas valores elimina de los dominios vecinos.
   b. Elige primero el que elimina menos (LCV).
3. Asigna el valor y continua.
```
