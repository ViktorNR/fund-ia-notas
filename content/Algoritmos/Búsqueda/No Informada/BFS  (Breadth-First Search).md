También llamado *Búsqueda en Anchura*, es un algoritmo de búsqueda no informada (ciega) que expande primero todos los nodos a una misma profundidad antes de pasar a la siguiente.

**Características:**
- Estructura: cola FIFO.
- Completo (si hay solución y el espacio es finito).
- Óptimo si todos los pasos cuestan 1 (camino más corto).
- Complejidad: tiempo y memoria O(b^d+1); b: branching factor, d: profundidad de la solución).


**Ventajas:**
- Encuentra la solución más corta (en número de pasos).
- Es sencilla de implementar.
- Garantiza completitud en espacios finitos.

**Desventajas:**
- Consume mucha memoria.
- Puede volverse ineficiente en problemas con gran factor de ramificación o solución profunda.

### Pseudocódigo
```python
from collections import deque

def BFS(inicio, objetivo, grafo):
    # Creamos una cola y añadimos el nodo inicial
    cola = deque([inicio])
    
    # Conjunto para marcar nodos ya visitados
    visitados = set([inicio])
    
    # (Opcional) Diccionario para reconstruir el camino
    padre = {inicio: None}

    while cola:
        # Tomamos el primer elemento de la cola (FIFO)
        nodo = cola.popleft()
        
        # Verificamos si encontramos el objetivo
        if nodo == objetivo:
            return reconstruir_camino(padre, objetivo)
        
        # Expandimos los vecinos del nodo actual
        for vecino in grafo[nodo]:
            if vecino not in visitados:
                visitados.add(vecino)
                padre[vecino] = nodo
                cola.append(vecino)
    
    return None  # No se encontró solución

def reconstruir_camino(padre, objetivo):
    camino = []
    nodo = objetivo
    while nodo is not None:
        camino.append(nodo)
        nodo = padre[nodo]
    return list(reversed(camino))
```