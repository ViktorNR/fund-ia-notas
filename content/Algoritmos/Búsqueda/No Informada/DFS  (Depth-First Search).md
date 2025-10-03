También llamado *Búsqueda en Profundidad*, es un algoritmo de búsqueda no informada que expande siempre el **nodo más profundo** de la frontera antes de retroceder.

**Características:**
- Estrategia: Explora un camino hasta el fondo antes de retroceder ("backtracking").
- Estructura: Pila (LIFO) -> puede implementarse con stack o recursión.
- Completitud:
	-  No siempre en espacio infinitos (puede quedar atascado en ramas infinitas).
	-  En espacios finitos, sí encuentra solución.
- Óptima: No garantiza la solución más corta.
- Complejidad temporal: O(b^m).
- Complejidad espacial: O(bm) - ventaja frente a BFS, mucho más eficiente en memoria.

**Ventajas:**
- Muy bajo consumo de memoria.
- Puede encontrar soluciones rápidamente si están en ramas profundas.
- Fácil de implementar (recursivo o con pila).

**Desventajas:**
- No es óptimo (puede encontrar un camino más largo aunque exista uno más corto).
- Puede no ser completa si el espacio de búsqueda es infinito y no hay control de ciclos.

### Pseudocodigo

```python
def DFS(inicio, objetivo, grafo):
    pila = [inicio]
    visitados = set([inicio])
    padre = {inicio: None}
    
    while pila:
        nodo = pila.pop()  # LIFO: último en entrar, primero en salir
        
        if nodo == objetivo:
            return reconstruir_camino(padre, objetivo)
        
        for vecino in grafo[nodo]:
            if vecino not in visitados:
                visitados.add(vecino)
                padre[vecino] = nodo
                pila.append(vecino)
    
    return None  # No se encontró solución
    
def reconstruir_camino(padre, objetivo):
    camino = []
    nodo = objetivo
    while nodo is not None:
        camino.append(nodo)
        nodo = padre[nodo]
    return list(reversed(camino))

```
