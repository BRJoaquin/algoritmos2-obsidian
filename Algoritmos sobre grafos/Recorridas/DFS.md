---
tag: algoritmo
---

La Búsqueda en Profundidad (Depth-First Search, DFS) es un algoritmo de recorrido de [[Grafo]] que explora el grafo siguiendo un camino desde el vértice origen hasta llegar a un vértice sin vecinos no visitados. Cuando se encuentra un vértice sin vecinos no visitados, el algoritmo retrocede a lo largo del camino hasta encontrar un vértice con vecinos no visitados y continúa la exploración desde allí. El proceso se repite hasta que se visitan todos los vértices alcanzables desde el vértice origen.

DFS puede ser implementado de forma recursiva o iterativa utilizando una pila. La versión recursiva suele ser más corta y fácil de entender, mientras que la versión iterativa puede ser más eficiente en términos de espacio. DFS se utiliza en una variedad de aplicaciones, como detectar ciclos en un grafo, encontrar componentes conexos, comprobar si un grafo es bipartito, y resolver problemas de búsqueda y optimización combinatoria.