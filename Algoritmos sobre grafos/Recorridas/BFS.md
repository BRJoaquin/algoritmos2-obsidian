---
tag: algoritmo
---

La Búsqueda en Anchura (Breadth-First Search, BFS) es un algoritmo de recorrido de grafos que explora los vértices de un [[Grafo]] en niveles, visitando todos los vértices a una distancia 'd' del vértice origen antes de visitar los vértices a una distancia 'd+1'. **El algoritmo BFS puede ser aplicado a grafos dirigidos o no dirigidos**, y se utiliza en una variedad de aplicaciones, como encontrar el camino más corto en un grafo no ponderado, determinar la conectividad de un grafo o realizar búsquedas en estructuras de datos jerárquicas como árboles y redes sociales.

El algoritmo BFS sigue estos pasos generales:

1.  Inicializar: Selecciona un vértice origen y crea una [[Cola]] vacía. Marca el vértice origen como encolado y lo encola.

2.  Explorar: Mientras la cola no esté vacía, realiza los siguientes pasos: 
		a. Desencola el siguiente vértice en la cola (llamémosle 'v'). 
		b. Procesa el vértice 'v' (por ejemplo, imprímelo, guárdalo en una lista de vértices visitados, etc.). 
		c. Encuentra todos los vértices adyacentes a 'v' que no han sido encolados y los marca como encolados. A continuación, encola estos vértices en la cola.

4.  Finalizar: Cuando la cola esté vacía, el algoritmo BFS habrá visitado todos los vértices alcanzables desde el vértice origen.


El algoritmo BFS garantiza que los vértices se visiten en orden de distancia desde el vértice origen. Por lo tanto, si existe un camino más corto entre el vértice origen y cualquier otro vértice del grafo, BFS lo encontrará. Además, BFS es un algoritmo eficiente en términos de tiempo y espacio, con una complejidad de tiempo $O(|V|+|E|)$ con listas de adyacencia ([[Grafo#Lista de adyacencia]], donde $|V|$ es el número de vértices en el grafo y $|E|$ es el número de aristas.

El algoritmo BFS puede ser adaptado fácilmente para abordar problemas específicos, como determinar si un grafo es bipartito, encontrar ciclos en un grafo o calcular la distancia entre dos vértices.

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Implementación de BFS en C++
void bfs(const Graph& graph, int origin) {
    int num_vertices = graph.size();
    vector<bool> enqueued(num_vertices, false);
    queue<int> q;

    // Marcar el vértice de origen como encolado y encolarlo
    enqueued[origin] = true;
    q.push(origin);

    while (!q.empty()) {
        int current_vertex = q.front();
        q.pop();

        // Procesar el vértice actual (por ejemplo, imprimirlo)
        cout << "Vértice visitado: " << current_vertex << endl;

        // Explorar los vértices adyacentes al vértice actual
        for (int neighbor : graph[current_vertex]) {
            if (!enqueued[neighbor]) {
                enqueued[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```