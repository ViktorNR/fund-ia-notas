---
title: Notas para Fundamentos de IA
draft: false
---
## ¿Qué es la Inteligencia Artificial?
"La IA es el estudio de los agentes que reciben percepciones del entorno y realizan acciones" - Russel & Norvig

**Definiciones clásicas:** pensamiento humano, compartamiento humano, pensamiento racional, comportamiento racional.


| Década   | Avances clave                                            |
| -------- | -------------------------------------------------------- |
| 1950s    | Turing, prueba de Turing, conferencia de Darmouth (1956) |
| 1960-70s | Primeros programas lógicos y de juegos.                  |
| 1980s    | Sistemas expertos (ej. MYCIN).                           |
| 1990s    | Modelos probabilísticos, redes bayesianas.               |
| 2000s +  | Big data, aprendizaje profundo, IA en producción masiva. |

| Desafio                   | Ejemplo / Implicación                            |
| ------------------------- | ------------------------------------------------ |
| Explicabilidad            | ¿Cómo saber por qué un modelo tomó una decisión? |
| Robustez y generalización | Fallos fuera de los datos conocidos.             |
| Ética y sesgo             | Algoritmos discriminatorios.                     |
| IA general                | Aún muy lejos de la inteligencia humana.         |

---

## Modelar un problema de búsqueda
Un problema de búsqueda se define por:

1. **Estado inicial:** punto de partida.
2. **Acciones posibles:** movimientos o transiciones válidas desde un estado.
3. **Modelo de transición:** define el estado resultando de aplicar una acción.
4. **Objetivo o prueba de objetivo:** condición que determina cuándo de ha encontrado una solución.
5. **Costo del camino (opcional):** valor asociado a alcanzar un estado.

## Problema del lobo, la cabra y la col

* El granjero debe cruzar un río llevando a los tres sin que se coman entre sí.
* Estados = qué hay en cada orilla.
* BFS/DFS exploran posibles secuencias de cruces.

### Elementos del modelo
**Estados.** Representamos en qué orilla está cada entidad. Usamos binarios par que sea simple:
* 0 = orilla izquierda, 1 = orilla derecha.
* Estado = tupla(G, L, O, C) = (granjero, lobo, overa, col).
* Estado inicial: (0, 0, 0, 0) — (todos a la izquierda).
* Objetivo: (1, 1, 1, 1) — (todos a la derecha).

**Acciones.** La barca siempre viaja con el granjero y puede llevar, además, a **exactamente uno** entre {lobo, oveja, col} o ir **solo**.
* G cruza solo.
* G+L; G+O, G+C.
Formalmente: elegir un subconjunto M de {G, L, O, C} talque G pertenezca a M y |M| pertenezca a {1, 2}, y todos los de M están en la misma orilla que G antes del cruce.

**Modelo de transición.** Si el granjero está en s (0 o 1), la acción "mover M" produce el nuevo estado invirtiendo el bit de todos en M:
- next[x] =  1 - cur[x] si x pertenece a M.
- next[x] = cur[x] si x **no** pertenece a M.

**Restricciones (estados inválidos).** No puede quedar la oveja sola con su "comida" si el granjero no está presente:
- Prohibido L y O juntos en una orilla sin G en esa orilla.
- Prohibido O y C juntos en una orilla sin G en esa orilla.
Chequeo práctico (para cada orilla b perteneciente a {0, 1}):
- Si `L == b and O == b and G != b` -> inválido
- Si `O == b and C == b and G != b` -> inválido.

**Test objetivo.** `state == (1, 1, 1, 1)`.

**Costo.** Uniforme: 1 por cruce (óptimo con BFS).

---
## [[Algoritmo de Búsqueda|Algoritmos de Búsqueda]]

