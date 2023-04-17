
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

Algunos ejemplos uso pueden ser:

1.  Redes sociales: Los grafos no dirigidos pueden ser utilizados para representar conexiones entre amigos en una red social, donde una arista entre dos nodos indica que ambos son amigos mutuos.

2.  Redes de transporte: Un grafo no dirigido puede representar una red de carreteras en la que cada nodo es una ciudad y cada arista representa una carretera bidireccional que conecta dos ciudades.
   
3.  Red de distribución eléctrica: Un grafo no dirigido puede representar una red de distribución eléctrica, donde los nodos son estaciones de transformación y las aristas representan las conexiones entre ellas, permitiendo el flujo de energía en ambas direcciones.


### Dirigido

En un grafo dirigido, las aristas tienen una dirección específica, lo que significa que van desde un nodo de origen hasta un nodo de destino.

![[Pasted image 20230417173015.png]]

> La cantidad de aristas posibles en un grafo dirigido de V vertices es $V^2$

Algunos ejemplos uso pueden ser:

1.  Red de sitios web: Un grafo dirigido puede representar la estructura de enlaces entre sitios web, donde cada nodo es una página web y cada arista dirigida representa un enlace de una página a otra.

2.  Organigrama empresarial: Un grafo dirigido puede representar la estructura jerárquica de una empresa, donde cada nodo es un empleado y las aristas dirigidas representan la relación de supervisión entre empleados.

3.  Análisis de dependencias: Los grafos dirigidos pueden ser utilizados para modelar las dependencias entre tareas en un proyecto o entre módulos en un software, donde los nodos representan tareas o módulos y las aristas dirigidas indican que una tarea o módulo depende de otro.

## Ponderación

**La ponderación en los grafos se refiere a asignar un valor numérico o "peso" a cada arista en el grafo**. Estos pesos pueden representar diversos atributos o propiedades de las conexiones entre nodos, como la distancia, el costo, el tiempo, la capacidad, entre otros. Un grafo con aristas ponderadas se denomina "grafo ponderado".

En un grafo ponderado, el peso de una arista puede influir en la solución de diferentes problemas, como la búsqueda del camino más corto entre dos nodos (vease: [[#Camino más corto]]),  o el cálculo del [[#Árbol de cubrimiento mínimo]]. Los algoritmos que trabajan con grafos ponderados toman en cuenta estos pesos para encontrar soluciones óptimas a estos problemas.

Por ejemplo, en el caso de una red de transporte, las aristas podrían estar ponderadas por la distancia entre dos ciudades o por el tiempo de viaje requerido. Entonces, al buscar el camino más corto entre dos ciudades, un algoritmo de grafo ponderado, como el algoritmo de [[Dijkstra]] o el algoritmo de [[Bellman-Ford]], tendría en cuenta estos pesos para determinar la ruta óptima.

Es importante mencionar que no todos los grafos son ponderados. En un grafo no ponderado, todas las aristas tienen el mismo peso implícito o se asume que no hay diferencias significativas entre las conexiones. En estos casos, los algoritmos de grafos se enfocan en las relaciones topológicas entre los nodos y no en los atributos de las aristas, por ejemplo [[Orden topologico]] o [[#Recorridas]] como [[BFS]] y [[DFS]].

![[Pasted image 20230417173841.png]]

> Cabe destacar que la ponderación y la dirección son propiedades **independientes**, es decir pueden existir las 4 combinaciones. 

## Ciclicidad

La ciclicidad en grafos se refiere a la presencia de ciclos en ellos. Un ciclo es un camino que comienza y termina en el mismo nodo, recorriendo al menos una arista y sin repetir aristas ni nodos intermedios. Los grafos pueden ser clasificados como cíclicos o acíclicos, según si contienen ciclos o no.

![[Pasted image 20230417174235.png]]

Grafo cíclico: Un grafo que contiene al menos un ciclo. 
Grafo acíclico: Un grafo que no contiene ciclos.

## Densidad

La densidad es una medida que describe **qué tan conectado está un grafo**. Se calcula como la proporción entre el número de conexiones (aristas) que realmente existen en el grafo y el número máximo de conexiones posibles entre todos los nodos.

La densidad de un grafo varía entre 0 y 1. Un valor de densidad cercano a 0 significa que el grafo es muy **disperso** y tiene pocas conexiones entre sus nodos. Por otro lado, un valor cercano a 1 indica que el grafo es muy **denso** y tiene muchas conexiones entre sus nodos, acercándose al máximo posible.

![[Pasted image 20230417175153.png]]



# Implementaciones

## Matriz de adyacencia


## Lista de adyacencia

# Recorridas


# Árbol de cubrimiento mínimo


# Camino más corto

