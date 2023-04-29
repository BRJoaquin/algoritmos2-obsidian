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

<iframe width="560" height="315" src="https://www.youtube.com/embed/x-VTfcmrLEQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

El algoritmo BFS garantiza que los vértices se visiten en orden de distancia desde el vértice origen. Por lo tanto, si existe un camino más corto entre el vértice origen y cualquier otro vértice del grafo, BFS lo encontrará. Además, BFS es un algoritmo eficiente en términos de tiempo y espacio, con una complejidad de tiempo $O(|V|+|E|)$ con listas de adyacencia ([[Grafo#Lista de adyacencia]], donde $|V|$ es el número de vértices en el grafo y $|E|$ es el número de aristas.

El algoritmo BFS puede ser adaptado fácilmente para abordar problemas específicos, como determinar si un grafo es bipartito, encontrar ciclos en un grafo o calcular la distancia entre dos vértices.

# Implementación

```cpp
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

# Visualización

https://www.cs.usfca.edu/~galles/visualization/BFS.html

# Usos

El algoritmo de Búsqueda en Anchura (Breadth-First Search, BFS) es un algoritmo de recorrido de grafos con diversas aplicaciones en ciencias de la computación y algoritmos. Algunas de las aplicaciones y usos más comunes del algoritmo BFS incluyen:

1.  Encontrar el camino más corto: BFS es útil para encontrar el camino más corto entre dos vértices en un grafo no ponderado, ya que explora todos los vértices a una distancia dada antes de pasar a los vértices a una distancia mayor.

2.  Encontrar componentes conexas: BFS puede ser utilizado para identificar los componentes conexas en un grafo no dirigido, similar a DFS. Al iniciar el algoritmo en cada vértice no visitado, se pueden explorar todos los vértices de un componente conexo antes de pasar al siguiente componente.

3.  Verificar si un grafo es bipartito: Mediante una adaptación del algoritmo BFS, se puede determinar si un grafo es bipartito (es decir, si se puede dividir en dos conjuntos disjuntos de vértices de modo que todas las aristas conecten vértices de un conjunto con vértices del otro).

4.  Niveles en un árbol o grafo: BFS puede ser utilizado para determinar los niveles en un árbol o grafo. Por ejemplo, en un árbol, BFS puede ayudar a determinar la profundidad de cada nodo con respecto al nodo raíz.

5.  Análisis de redes sociales: BFS es útil para analizar redes sociales y calcular métricas como la distancia promedio entre nodos, la centralidad de cercanía y la centralidad de intermediación.

## Ejemplo de uso: camino más corto

