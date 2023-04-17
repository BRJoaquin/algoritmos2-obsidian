
Los grafos es un [[Tipo Abstracto de Dato (TAD)]] no lineal que consiste en un conjunto de nodos (también llamados vértices) y un conjunto de enlaces (también llamados aristas o arcos) que conectan estos nodos. Los grafos son una forma de representar relaciones y conexiones entre elementos de un conjunto

![[Pasted image 20230417172830.png]]

> |V| representa la cantidad de nodos (vértices) en un grafo, mientras que |A| o |E| representa la cantidad de aristas en el mismo grafo.

# Clasificaciones

## Dirección 

La direccionalidad de un grafo se refiere a si las aristas tienen una dirección específica (grafo dirigido) o si son bidireccionales (grafo no dirigido). La cantidad de aristas posibles en cada caso depende del número de nodos presentes en el grafo.

### No dirigido

En un grafo no dirigido, una arista conecta dos nodos de manera bidireccional, lo que significa que no hay distinción entre el nodo de origen y el nodo de destino.

![[Pasted image 20230417172933.png]]

> La cantidad de aristas posibles en un grafo no dirigido de V vertices es $V + \frac{V(V-1)}{2}$




### Dirigido
En un grafo dirigido, las aristas tienen una dirección específica, lo que significa que van desde un nodo de origen hasta un nodo de destino.

![[Pasted image 20230417173015.png]]

> La cantidad de aristas posibles en un grafo dirigido de V vertices es $V^2$

## Ponderación



# Implementaciones

## Matriz de adyacencia


## Lista de adyacencia

# Recorridas


# Árbol de cubrimiento mínimo


# Camino mas corto

