Un algoritmo de búsqueda en Inteligencia Artificial es un procedimiento sistemático que, partiendo de un **estado inicial** y conociendo las **acciones posibles** y un **objetivo**, explora el **espacio de estados** generado por el modelo de transición, con el fin de encontrar una **secuencia de acciones (plan)** que lleve desde el estado inicial hasta un estado objetivo, optimizando según una medida de rendimiento (ej: costo, tiempo, pasos).

## Componentes Clave

1. **Espacio de estados** -> conjunto de todas las configuraciones alcanzables del problema.
2. **Nodo** -> representación de un estado dentro del árbol de búsqueda, con información adicional (padre, acción, costo g).
3. **Frontera** -> estructura de datos que guarda los nodos por expandir (cola, pila, prioridad).
4. **Expansión** -> proceso de aplicar las acciones al estado de un nodo y generar sus sucesores.
5. **Estrategia de selección** -> criterio para decidir qué nodo expandir (ej: [[BFS  (Breadth-First Search)|BFS]] usa FIFO, [[DFS  (Depth-First Search)|DFS]] usa LIFO, [[AStar (A estrella o A asterísco)|A*]] usa $f = g + h$).

### Clasificación General
- **No informados (ciega)** $\to$ no usan conocimiento adicional del objetivo ([[BFS  (Breadth-First Search)|BFS]], [[DFS  (Depth-First Search)|DFS]], UCS).
- **Informados** (con [[Heurística|heurística]]) $\to$ aprovechan estimaciones del objetivo (Greedy, [[AStar (A estrella o A asterísco)|A*]], IDA*).

