---
tag: estructura_de_datos
---

La [[Estructura de datos]] Disjoint-set (MFset en el curso) es una estructura que permite mantener un conjunto de elementos particionados en subconjuntos disjuntos y realizar operaciones de unión y búsqueda en estos subconjuntos de manera eficiente. La idea principal detrás de esta estructura de datos es mantener información sobre las conexiones entre los elementos en lugar de almacenar explícitamente los conjuntos.

![[Pasted image 20230429114258.png]]

Las operaciones principales en una estructura Disjoint-set son:

1.  Find(x): Esta operación encuentra el representante del conjunto al que pertenece el elemento x. Los elementos que pertenecen al mismo conjunto tendrán el mismo representante. Esta operación se utiliza para determinar si dos elementos están en el mismo conjunto o no.

2.  Union(x, y): Esta operación combina los conjuntos que contienen los elementos x e y en un nuevo conjunto. Si x e y ya están en el mismo conjunto, no se realiza ninguna acción.

La estructura Disjoint-set se implementa comúnmente utilizando una técnica llamada "union by rank with path compression". En esta técnica, cada elemento mantiene un enlace a su padre y un rango (que es una medida de la profundidad del árbol que representa el conjunto). Los elementos se organizan en forma de árboles, donde cada árbol representa un conjunto y la raíz del árbol es el representante del conjunto.

-   Union by rank: Al realizar la operación Union, **se unen los árboles basándose en sus rangos (alturas)**. El árbol con menor rango se une al árbol con mayor rango (altura del arbol). Si ambos árboles tienen el mismo rango, se unen, y el rango del árbol resultante se incrementa en uno. Esto ayuda a mantener la altura de los árboles pequeña, lo que mejora la eficiencia de las operaciones.

-   Path compression: La compresión de caminos es una optimización de la operación Find. Durante la búsqueda del representante de un elemento, **se actualiza el enlace de cada elemento visitado en el camino para que apunte directamente al representante del conjunto**. Esto acelera las búsquedas futuras y mejora el rendimiento en general.

La estructura de datos Disjoint-set se utiliza a menudo en algoritmos de grafos, como [[Kruskal]] para encontrar el árbol de cubrimiento mínimo ([[Grafo#Árbol de cubrimiento mínimo]]) o para detectar ciclos en un grafo no dirigido. También puede ser útil en otras aplicaciones donde se requiere mantener información sobre conjuntos disjuntos y realizar operaciones de unión y búsqueda de manera eficiente.

# Visualización

https://www.cs.usfca.edu/~galles/visualization/DisjointSets.html

# Implementación

```cpp
#include <vector>

class DisjointSet {
public:
    DisjointSet(int size) {
        parent.resize(size);
        rank.resize(size, 0);
        for (int i = 0; i < size; ++i) {
            parent[i] = i;
        }
    }

    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]); // Compress path
        }
        return parent[x];
    }

    void union_sets(int x, int y) {
        int root_x = find(x);
        int root_y = find(y);

        if (root_x == root_y) {
            return; // Already in the same set
        }

        if (rank[root_x] > rank[root_y]) {
            parent[root_y] = root_x;
        } else {
            parent[root_x] = root_y;
            if (rank[root_x] == rank[root_y]) {
                ++rank[root_y];
            }
        }
    }

private:
    std::vector<int> parent;
    std::vector<int> rank;
};
```


# Más info

- https://www.geeksforgeeks.org/disjoint-set-data-structures/
- https://en.wikipedia.org/wiki/Disjoint-set_data_structure
