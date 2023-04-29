---
tag: algoritmo
---

La Búsqueda en Profundidad (Depth-First Search, DFS) es un algoritmo de recorrido de [[Grafo]] que explora el grafo siguiendo un camino desde el vértice origen hasta llegar a un vértice sin vecinos no visitados. Cuando se encuentra un vértice sin vecinos no visitados, el algoritmo retrocede a lo largo del camino hasta encontrar un vértice con vecinos no visitados y continúa la exploración desde allí. El proceso se repite hasta que se visitan todos los vértices alcanzables desde el vértice origen.

DFS puede ser implementado de forma recursiva o iterativa utilizando una pila. La versión recursiva suele ser más corta y fácil de entender, mientras que la versión iterativa puede ser más eficiente en términos de espacio. DFS se utiliza en una variedad de aplicaciones, como detectar ciclos en un grafo, encontrar componentes conexos, comprobar si un grafo es bipartito, y resolver problemas de búsqueda y optimización combinatoria.

<iframe width="560" height="315" src="https://www.youtube.com/embed/NUgMa5coCoE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Implementación

```cpp
// Función auxiliar para el algoritmo DFS recursivo
void dfs_recursive(const Graph& graph, int current_vertex, vector<bool>& visited) {
    // Marcar el vértice actual como visitado
    visited[current_vertex] = true;

    // Procesar el vértice actual (por ejemplo, imprimirlo)
    cout << "Vértice visitado: " << current_vertex << endl;

    // Explorar los vértices adyacentes al vértice actual
    for (int neighbor : graph[current_vertex]) {
        if (!visited[neighbor]) {
            dfs_recursive(graph, neighbor, visited);
        }
    }
}

void dfs(const Graph& graph, int origin) {
    int num_vertices = graph.size();
    // crea un array de tamaño V con valor false en todos sus elementos
    vector<bool> visited(num_vertices, false);

    dfs_recursive(graph, origin, visited);
}
```

# Visualización

https://www.cs.usfca.edu/~galles/visualization/DFS.html

