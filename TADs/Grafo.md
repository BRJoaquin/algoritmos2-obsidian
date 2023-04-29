
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

> [!warning]
> Esta clasificación es muy importante para nosotros ya que puede determinar como implementamos los grafos

La relación entre la densidad de un grafo y las dos implementaciones ([[#Lista de adyacencia]] y [[#Matriz de adyacencia]]) radica principalmente en la **eficiencia de espacio y en el rendimiento de las operaciones realizadas en el grafo**.

Para grafos **dispersos** (baja densidad), la **lista de adyacencia** suele ser más eficiente en términos de espacio y rendimiento, ya que almacena **solo las aristas existentes**, lo que resulta en un menor consumo de memoria. **Además, las operaciones como recorrer los vecinos de un nodo son más rápidas en una lista de adyacencia** ($O(V)$ como peor caso).

Por otro lado, para grafos **densos** (alta densidad), la **matriz de adyacencia** puede ser una opción más adecuada, ya que la matriz estará mayormente llena de valores distintos de cero (o del valor que se haya elegido para la ausencia de arista). Aunque consume más memoria que la lista de adyacencia, permite acceder rápidamente a la información de adyacencia entre dos nodos específicos.

## Conexidad

La conexidad es una propiedad de los grafos que indica si hay un camino entre cada par de nodos en el grafo.

Un **grafo no dirigido es conexo** **si existe al menos un camino entre cada par de nodos**. Es decir, se puede llegar desde cualquier nodo a cualquier otro nodo del grafo siguiendo las aristas. Si un grafo no es conexo, se considera desconexo.

En el caso de **grafos dirigidos,** la noción de conexidad se extiende a la idea de "**fuertemente conexo**" y "**débilmente conexo**". **Un grafo dirigido es fuertemente conexo si existe un camino dirigido entre cada par de nodos**, es decir, se puede llegar de un nodo a otro siguiendo las aristas en su dirección. **Un grafo dirigido es débilmente conexo si se vuelve conexo al ignorar la dirección de las aristas**.

La conexidad es una propiedad importante en el análisis de grafos, ya que puede afectar la solución de problemas como la búsqueda del [[#Camino más corto]], o la identificación de puntos críticos en una red.

# Implementaciones

En general, las implementaciones de grafos buscan representar de manera eficiente la estructura y las conexiones entre los nodos. Existen diferentes enfoques para implementar grafos, y cada uno tiene sus ventajas y desventajas en términos de eficiencia de espacio, rendimiento y facilidad de uso. Algunas implementaciones son más adecuadas para ciertos tipos de grafos o problemas específicos.

Al elegir una implementación, es importante considerar factores como la **densidad del grafo**, las **operaciones que se realizarán con más frecuencia** y las restricciones de memoria y tiempo de ejecución. También es fundamental tener en cuenta si el grafo es dirigido o no dirigido, ponderado o no ponderado.

Las opciones de implementación de grafos más comunes son:
1. Matriz de adyacencia
2. Lista de adyacencia

![[Pasted image 20230417180414.png]]

## Matriz de adyacencia

La matriz de adyacencia es una forma común de representar grafos en la que se utiliza una matriz cuadrada para indicar las conexiones (aristas) entre los nodos. La matriz tiene un tamaño de |V| x |V|, donde |V| es el número de nodos en el grafo. Cada entrada (i, j) en la matriz representa la relación entre el nodo i y el nodo j.

En un grafo no dirigido, la matriz de adyacencia es simétrica, lo que significa que si hay una arista entre el nodo i y el nodo j, entonces la matriz contendrá un valor no nulo (generalmente 1) tanto en la posición (i, j) como en la posición (j, i). En un grafo dirigido, la simetría no se garantiza, ya que la conexión entre los nodos puede ser unidireccional.

En el caso de grafos ponderados, la matriz de adyacencia almacena los pesos de las aristas en lugar de simplemente indicar la presencia o ausencia de una arista. En este caso, las entradas (i, j) de la matriz contienen el peso de la arista que conecta el nodo i con el nodo j. Si no hay conexión entre los nodos, se utiliza un valor especial, como 0, infinito o un número negativo grande, según el contexto.

La matriz de adyacencia es especialmente útil en grafos densos, donde la mayoría de los pares de nodos están conectados, ya que permite un acceso rápido a la información de conexión entre nodos específicos. Sin embargo, en grafos dispersos, esta representación puede ser ineficiente en términos de espacio, ya que la mayoría de las entradas de la matriz estarán vacías (sin aristas) y se desperdicia memoria almacenando información innecesaria.

![[Pasted image 20230417181130.png]]

## Lista de adyacencia

La lista de adyacencia es una forma común de representar grafos, en la que cada nodo tiene asociada una lista de los nodos adyacentes, es decir, aquellos con los que comparte una arista. Esta representación es especialmente útil en grafos dispersos, donde la mayoría de los pares de nodos no están conectados, ya que consume menos memoria que la matriz de adyacencia.

En una lista de adyacencia, se mantiene una lista principal que contiene tantos elementos como nodos haya en el grafo. Cada elemento de esta lista principal es, a su vez, una lista que contiene los nodos adyacentes al nodo correspondiente. En el caso de grafos no dirigidos, si el nodo i está en la lista de adyacencia del nodo j, entonces el nodo j también estará en la lista de adyacencia del nodo i. Para grafos dirigidos, la lista de adyacencia solo contiene información sobre las aristas dirigidas desde un nodo hacia otros nodos.

Para grafos ponderados, la lista de adyacencia puede almacenar no solo los nodos adyacentes, sino también los pesos asociados a las aristas. Esto se logra almacenando pares de valores en la lista de adyacencia, donde el primer elemento del par es el nodo adyacente y el segundo elemento es el peso de la arista.

Las listas de adyacencia son una representación eficiente para realizar operaciones como recorrer todos los vecinos de un nodo, ya que solo es necesario iterar sobre los elementos de la lista de adyacencia de ese nodo en particular. Sin embargo, acceder a la información de conexión entre dos nodos específicos puede ser menos eficiente en comparación con la matriz de adyacencia, ya que es necesario buscar en la lista de adyacencia en lugar de acceder a una posición específica en la matriz.

![[Pasted image 20230417181221.png]]

# Recorridas

El recorrido de grafos es una técnica fundamental en la teoría de grafos y en la ciencia de la computación en general. Se utilizan diferentes algoritmos para visitar todos los vértices de un grafo, comenzando desde un vértice origen y siguiendo un criterio específico de exploración. Los dos algoritmos más comunes para recorrer grafos son la Búsqueda en Anchura (Breadth-First Search, [[BFS]]) y la Búsqueda en Profundidad (Depth-First Search, [[DFS]]).

Ambos algoritmos, [[BFS]] y [[DFS]], pueden ser implementados de manera iterativa o recursiva, y suelen utilizarse en combinación con estructuras de datos como [[#Lista de adyacencia]], [[#Matriz de adyacencia]] para representar los grafos. Además, los algoritmos de recorrido de grafos pueden modificarse fácilmente para abordar problemas específicos y proporcionar información adicional sobre la estructura y propiedades de un grafo.

![[1_GT9oSo0agIeIj6nTg3jFEA.gif]]

# Árbol de cubrimiento mínimo


# Camino más corto

