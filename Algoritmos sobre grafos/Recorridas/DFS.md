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

# Usos

El algoritmo de Búsqueda en Profundidad (Depth-First Search, DFS) es una técnica de recorrido de grafos que se utiliza en una amplia variedad de aplicaciones en ciencias de la computación y algoritmos. Algunas de las aplicaciones y usos más comunes del algoritmo DFS incluyen:

1.  Detectar ciclos en un grafo: DFS puede ser utilizado para detectar la presencia de ciclos en un grafo, lo cual es útil para determinar si un grafo es un árbol (grafo acíclico y conexo) o para verificar si un grafo dirigido es un DAG (grafo acíclico dirigido).

2.  Encontrar componentes conexos: DFS puede ser empleado para identificar los componentes conexos de un grafo no dirigido. Al iniciar el algoritmo en cada vértice no visitado, se pueden explorar todos los vértices de un componente conexo antes de pasar al siguiente componente.

3.  Comprobar si un grafo es bipartito: Mediante una adaptación del algoritmo DFS, se puede determinar si un grafo es bipartito (es decir, si se puede dividir en dos conjuntos disjuntos de vértices de modo que todas las aristas conecten vértices de un conjunto con vértices del otro).

4.  Encontrar caminos entre dos vértices: DFS puede ser utilizado para encontrar un camino entre dos vértices en un grafo, aunque no garantiza encontrar el camino más corto como lo hace BFS.

5.  Topological sorting: En grafos dirigidos acíclicos (DAG), DFS puede ser adaptado para producir una ordenación topológica de los vértices, que es un orden lineal de los vértices de manera que para cada arista (u, v), el vértice u viene antes que el vértice v en el ordenamiento.

## Ejemplo de uso: bipartita

Para determinar si un grafo es [bipartito](https://es.wikipedia.org/wiki/Grafo_bipartito) utilizando DFS, se pueden asignar colores a los vértices durante el recorrido. Si en algún momento un vértice ya coloreado es visitado con el mismo color que su vecino, entonces el grafo no es bipartito.

![[Pasted image 20230429111711.png]]

```cpp
// Función auxiliar para el algoritmo DFS que verifica si un grafo es bipartito
bool is_bipartite_dfs(const Graph& graph, int current_vertex, vector<int>& colors, int current_color) {
    // Asignar el color actual al vértice actual
    colors[current_vertex] = current_color;

    // Explorar los vértices adyacentes al vértice actual
    for (int neighbor : graph[current_vertex]) {
        if (colors[neighbor] == -1) {
            // Si el vecino no está coloreado, asignarle el color opuesto y continuar el recorrido
            if (!is_bipartite_dfs(graph, neighbor, colors, 1 - current_color)) {
                return false;
            }
        } else if (colors[neighbor] == current_color) {
            // Si el vecino ya está coloreado y tiene el mismo color que el vértice actual, el grafo no es bipartito
            return false;
        }
    }

    // Si todos los vecinos tienen colores opuestos al vértice actual, el grafo es bipartito hasta ahora
    return true;
}

// Función que utiliza DFS para verificar si un grafo es bipartito
bool is_bipartite(const Graph& graph) {
    int num_vertices = graph.size();
    vector<int> colors(num_vertices, -1);

    for (int i = 0; i < num_vertices; ++i) {
        if (colors[i] == -1) {
            if (!is_bipartite_dfs(graph, i, colors, 0)) {
                return false;
            }
        }
    }

    return true;
}
```

## Ejemplo de uso: cantidad de componentes conexas

![[Pasted image 20230429111600.png]]

Para determinar la cantidad de componentes conexas en un grafo no dirigido utilizando DFS, podemos iniciar un recorrido DFS desde cada vértice no visitado y contar cuántas veces se realizó el recorrido.

```cpp
// Función auxiliar para el algoritmo DFS recursivo
void dfs_recursive(const Graph& graph, int current_vertex, vector<bool>& visited) {
    // Marcar el vértice actual como visitado
    visited[current_vertex] = true;

    // Explorar los vértices adyacentes al vértice actual
    for (int neighbor : graph[current_vertex]) {
        if (!visited[neighbor]) {
            dfs_recursive(graph, neighbor, visited);
        }
    }
}

// Función que utiliza DFS para contar el número de componentes conexas en un grafo no dirigido
int count_connected_components(const Graph& graph) {
    int num_vertices = graph.size();
    vector<bool> visited(num_vertices, false);
    int connected_components_count = 0;

    for (int i = 0; i < num_vertices; ++i) {
        if (!visited[i]) {
            dfs_recursive(graph, i, visited);
            ++connected_components_count;
        }
    }

    return connected_components_count;
}
```