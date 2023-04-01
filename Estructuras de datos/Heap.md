---
tag: estructura_de_datos
---

# Intro

Un heap binario es una [[Estructura de datos]] de tipo árbol binario que cumple con dos propiedades fundamentales:

1.  **Propiedad estructural**: Es un árbol binario completo, excepto quizás en el último nivel, donde los nodos pueden no estar presentes a la derecha. Esto significa que todos los niveles del árbol, excepto posiblemente el último, están completamente llenos de nodos, y los nodos en el último nivel están lo más a la izquierda posible.

![[Pasted image 20230401085607.jpg]]


> Cada nodo tiene tres posibilidades:
> 1) No tener hijos (hoja).
>    Ejemplos: 44, 35, 33, 42, 27
> 2) Tener ambos hijos
>    Ejemplos: 10, 14, 19, 26
> 3) Tener solo hijo izquierdo. En este caso el hundir de un nodo se compara con dicho nodo.
>    Ejemplo: 33 (solo se puede tener uno de estos nodos)
>
> Debido a la propiedad estructural de un heap es imposible **solo** tener hijo derecho.


3.  **Propiedad de orden**: El árbol binario satisface una condición de orden específica, lo que hace que sea un "min-heap" o un "max-heap". En un min-heap, cada nodo tiene un valor que es menor o igual que el valor de sus hijos. Esto implica que el nodo con el valor más pequeño siempre estará en la raíz del árbol. Por otro lado, en un max-heap, cada nodo tiene un valor mayor o igual que el valor de sus hijos, lo que significa que el nodo con el valor más grande siempre estará en la raíz del árbol.
   
![[Pasted image 20230401085720.png]]

> A diferencia de un ABB o un AVL, los Heap **NO** presenentan relación entre hijo izquierdo e hijo derecho. La relación esta dada por padre <-> hijos

# Usos

Un heap se utiliza en una variedad de aplicaciones y algoritmos debido a sus propiedades y eficiencia en ciertas operaciones. Algunos de los usos más comunes de un heap incluyen:

1.  **Colas de prioridad:** Un heap es una excelente estructura de datos para implementar [[Cola de prioridad]], que permiten acceder, insertar y eliminar elementos según sus prioridades de manera eficiente. Las colas de prioridad son útiles en situaciones donde se necesita manejar tareas o eventos con diferentes niveles de importancia.

2.  **Algoritmo de Dijkstra**: El heap se utiliza en el algoritmo de [[Dijkstra]] para encontrar el camino más corto en un grafo con pesos en las aristas. El algoritmo utiliza una cola de prioridad/heap para seleccionar el siguiente nodo a visitar en función de las distancias acumuladas desde el nodo inicial.

3.  **Algoritmo de Prim**: El algoritmo de [[Prim]], que encuentra el árbol de cubrimiento mínimo en un grafo conectado con pesos en las aristas, también utiliza un heap para seleccionar la arista de menor peso en cada iteración del algoritmo.

4.  **Heapsort**: Un heap puede ser utilizado en el algoritmo de ordenamiento llamado [[Heapsort]]. Este algoritmo aprovecha las propiedades del heap para ordenar una secuencia de elementos en tiempo O(n log n). Aunque heapsort no es tan rápido en la práctica como otros algoritmos de ordenamiento, como el [[Quicksort]] o el [[Mergesort]], tiene la ventaja de ser un algoritmo de ordenamiento in situ (no requiere memoria adicional) y su tiempo de ejecución es garantizado en O(n log n).

# Operaciones

Los heaps tienen tres operaciones básicas pero suficientes para cubrir muchos casos de uso.

## Inserción (insert)

Este método permite agregar un nuevo elemento al heap, manteniendo sus propiedades de forma y orden. La inserción generalmente se realiza agregando el elemento al final del heap y luego "flotándolo" hacia arriba (haciendo intercambios con su nodo padre) hasta que se cumpla la propiedad de orden.

### Proceso

1.  **Agregar el nuevo elemento al final del heap**: Colocar el elemento en la siguiente posición disponible en el último nivel del árbol binario o como el primer elemento en el nuevo nivel si el último nivel ya está completo. 

> Esto hace que la propiedad estructural ya este cumplida, y solo nos preocupamos por la propiedad de orden

2.  **Flotar** el elemento hacia arriba (Up-Heap): Comparar el valor del nuevo elemento con el valor de su nodo padre. Si el valor del nuevo elemento es menor que el valor del nodo padre (en el caso de un min-heap), intercambiar el nuevo elemento y el nodo padre. 
   Repetir este proceso, moviéndose hacia arriba en el árbol, hasta que se cumpla una de las siguientes condiciones:
		a. El nuevo elemento alcanza la raíz del árbol (es decir, ya no tiene un nodo padre). 
		b. El valor del nuevo elemento es mayor o igual que el valor de su nodo padre, lo que significa que la propiedad de orden del min-heap se mantiene.

### Ejemplo (min-heap)

Supongamos que tenemos el siguiente min-heap:

```
        10
       /  \
     15    20
    /  \   / \
   30  40 50  60
```

Ahora, queremos insertar el número 8 en el min-heap. Aquí está el proceso paso a paso:

1.  Agregar el nuevo elemento al final del heap:

```
        10
       /  \
     15    20
    /  \   / \
   30  40 50  60
  /
 8
```

2.  Flotar el elemento hacia arriba (Up-Heap):

Comparamos el nuevo elemento (8) con su nodo padre (30) y realizamos un intercambio porque 8 es menor que 30:

```
        10
       /  \
     15     20
    /  \   / \
   8  40 50  60
  /
 30
```

Continuamos flotando el elemento hacia arriba, ahora comparamos el nuevo elemento (8) con su nuevo nodo padre (15) y realizamos un intercambio porque 8 es menor que 15:

```
        10
       /  \
     8    20
    /  \   / \
   15  40 50  60
  /
 30
```

Por ultimo comparamos con su padre (10) y volvemos a intercambiar

```
        8
       /  \
     10    20
    /  \   / \
   15  40 50  60
  /
 30
```

Ahora, el proceso de inserción ha terminado, ya que hemos mantenido las propiedades de forma y orden del min-heap después de insertar el nuevo elemento.

## Eliminar (deletePeek)

El método `deletePeek` (a veces llamado `extract-min` para un min-heap o `extract-max` para un max-heap) se utiliza para eliminar y devolver el elemento en la raíz del heap. Es decir el menor elemento en caso de min-heap.

## Proceso

1.  **Intercambiar** el elemento prioritario (raíz) con el último elemento del heap.
2.  **Eliminar el último elemento** del heap (que era la raíz original).
3.  Hacer un proceso de **hundir** hacia abajo (Down-Heap) para mantener las propiedades de orden: 
   a. Comparar el elemento en la raíz con sus nodos hijos y encontrar el menor de ellos (en un min-heap, sino el mayor de ellos). 
   b. Si el elemento en la raíz es mayor que el menor de sus nodos hijos, intercambiar el elemento en la raíz con el menor de sus nodos hijos. 
   c. Repetir los pasos (a) y (b) hasta que el elemento en la raíz sea menor que ambos nodos hijos o no tenga más nodos hijos.

Este proceso garantiza que el elemento prioritario se elimine del heap y que se mantengan las propiedades de forma y orden del heap.

> Hay que tener en cuenta que un nodo puede tener solo hijo izquierdo.

### Ejemplo

Supongamos que tenemos el siguiente min-heap:

```
        10
       /  \
     15    20
    /  \   / \
   30  40 50  60
```

A continuación, se muestra el proceso de eliminar el elemento prioritario paso a paso:

1.  Intercambie el elemento prioritario (raíz) con el último elemento del heap:

```
        60
       /  \
     15    20
    /  \   / \
   30  40 50  10
```

2.  Elimine el último elemento del heap (anteriormente la raíz):

```
        60
       /  \
     15    20
    /  \   /
   30  40 50
```

3.  Hunda el elemento en la raíz hacia abajo (Down-Heap) para mantener las propiedades de orden del heap:

Comparamos el elemento en la raíz (60) con sus nodos hijos (15 y 20) y encontramos el menor (15). Intercambiamos 60 con 15:

```
        15
       /  \
     60    20
    /  \   /
   30  40 50
```

Continuamos hundiendo hacia abajo y comparamos 60 con sus nodos hijos (30 y 40), encontramos el menor (30) e intercambiamos 60 con 30:

```
        15
       /  \
     30    20
    /  \   /
   60  40 50
```

El proceso de hundir hacia abajo ha terminado, ya que 60 es hoja (no tiene hijos).

## Tope (peek)

El método `peek` es una operación simple en un heap (ya sea min-heap o max-heap) que devuelve el elemento prioritario sin eliminarlo del heap. El elemento prioritario es el que se encuentra en la raíz del árbol.

Para un min-heap, el elemento prioritario es el elemento con el valor mínimo, mientras que para un max-heap, es el elemento con el valor máximo.

En el ejemplo de min-heap que hemos estado utilizando, el heap se ve así:

```
        15
       /  \
     30    20
    /  \   /
   60  40 50
```

Al usar el método `peek` en este min-heap, simplemente devolveríamos el valor en la raíz del árbol, que en este caso es 15, sin modificar la estructura del heap.

El método `peek` es útil cuando solo necesitas conocer el elemento de la raiz sin eliminarlo o modificar la estructura del heap. La complejidad de tiempo para esta operación es O(1), ya que solo implica acceder al primer elemento del heap.

# Ordenes temporales
| Operación  | Complejidad de tiempo |
|------------|-----------------------|
| Insert     | O(1)cp / O(log n)pc              |
| DeletePeek (Extract-Min/Max) | O(log n) |
| Peek       | O(1)                  |

Explicación:

-   **Insert**: La operación de inserción tiene una complejidad de tiempo de O(log n) en el peor de los casos. Esto se debe a que en el peor de los casos, el elemento insertado puede tener que flotar hacia arriba (Up-Heap) hasta la raíz del árbol, lo que implica atravesar la altura del árbol. La altura de un heap binario completo es logarítmica con respecto al número de elementos (n) en el heap.
  En la mayoría de los casos, el número de intercambios que se deben realizar es pequeño. La altura del árbol es `log_2(n)`, donde n es el número de nodos. Sin embargo, la probabilidad de que se necesiten `log_2(n)` intercambios es baja, ya que es más probable que el elemento que estamos insertando no tenga que recorrer todo el camino hasta la raíz.
  
  > **véase:** [Average Case Analysis of Heap Building by Repeated Insertion](https://web.archive.org/web/20160205023201/http://www.stats.ox.ac.uk/__data/assets/pdf_file/0015/4173/heapbuildjalg.pdf)
  
  En términos más matemáticos, si analizamos el número de intercambios esperados en la inserción, resulta ser una serie geométrica que converge a una suma finita, lo que implica un tiempo promedio constante.
  
  > `1 + 1/2 + 1/4 + 1/8 + ... = 2`

-   **DeletePeek (Extract-Min/Max)**: La operación de eliminar y devolver el elemento prioritario tiene una complejidad de tiempo de O(log n). Esto se debe a que en el peor de los casos, el elemento intercambiado con la raíz puede tener que hundirse hacia abajo (Down-Heap) hasta la hoja más profunda del árbol, lo que implica atravesar la altura del árbol, que es logarítmica con respecto al número de elementos (n) en el heap.
  
  > A diferencia de la operación insertar, es muy probable que un elemento que el elemento que se hunde desde la raíz vuelva a estar en lo últimos niveles por lo cual **no** tiene un O(1)cp

-   **Peek**: La operación de obtener el elemento prioritario sin eliminarlo tiene una complejidad de tiempo constante O(1), ya que solo implica acceder al primer elemento del heap (la raíz), sin realizar ninguna otra operación o modificación en la estructura del heap.


# Contras / mal uso

Un heap no es la estructura de datos más adecuada para ciertas operaciones, especialmente cuando se trata de buscar o eliminar un elemento específico que no sea la raíz. Esto se debe a las siguientes razones:

1.  **Búsqueda ineficiente**: A diferencia de otras estructuras de datos como árboles binarios de búsqueda (BST) o tablas hash, un heap no está diseñado para proporcionar búsquedas rápidas de elementos arbitrarios. La búsqueda de un elemento específico en un heap puede tomar un tiempo de O(n) en el peor de los casos, ya que es posible que tenga que recorrer todos los elementos del árbol.

2.  **Eliminación ineficiente de elementos específicos**: Eliminar un elemento específico que no sea la raíz en un heap puede ser costoso en términos de tiempo. Primero, debe encontrar el elemento en el heap, lo que puede llevar O(n) en el peor de los casos. Luego, debe eliminar el elemento y restaurar las propiedades del heap, lo que puede tomar un tiempo de O(log n). Por lo tanto, eliminar un elemento específico en un heap puede tener una complejidad de tiempo total de O(n).

Dado que un heap está diseñado principalmente para mantener el orden parcial (mínimo o máximo) y no proporciona un acceso eficiente a elementos arbitrarios, no es la estructura de datos más adecuada para operaciones que requieren buscar o eliminar elementos específicos. En tales casos, es posible que desee considerar otras estructuras de datos, como árboles binarios de búsqueda, tablas hash o árboles balanceados, que ofrecen búsquedas y eliminaciones más eficientes para elementos específicos.

# Implementación con array

![[Pasted image 20230401102534.png]]

Un heap binario puede ser representado de manera eficiente utilizando un array lineal, mapeando los nodos del árbol a elementos en el array. Este mapeo se realiza siguiendo un orden de nivel (también conocido como recorrido por niveles), es decir, se recorre cada nivel del árbol de izquierda a derecha.

Aquí está cómo se realiza el mapeo:

1.  El primer elemento del array (índice 0) representa la raíz del árbol.
   
   > [!warning]
   > También es posible implementar el heap donde la raíz se encuentra en la posición 1.
   > Esto tiene consecuencias en manejo de indices como por ejemplo el calculo de la posiscion de los hijos y padre.
   
   
1.  Para cada elemento en el array con índice `i`:
    -   El hijo izquierdo del elemento se encuentra en la posición `2 * i + 1`.
    -   El hijo derecho del elemento se encuentra en la posición `2 * i + 2`.
    -   El padre del elemento se encuentra en la posición `(i - 1) / 2` (redondeado hacia abajo en caso de división entera).

> De tener la raiz en la posición 1 quedaría:
>	-   El hijo izquierdo del elemento se encuentra en la posición `2 * i.`
>	-   El hijo derecho del elemento se encuentra en la posición `2 * i + 1`.
>	-   El padre del elemento se encuentra en la posición `i / 2` (redondeado hacia abajo en caso de división entera).

Tomemos un ejemplo de un min-heap y veamos cómo se mapea con un array:

```
        10
       /  \
     20    30
    /  \
   40  50
```

Array: `[10, 20, 30, 40, 50]`

Mapeo:

-   La raíz del árbol (10) se almacena en la posición 0 del array.
-   El hijo izquierdo de 10 (20) se almacena en la posición 1 del array (2 * 0 + 1 = 1).
-   El hijo derecho de 10 (30) se almacena en la posición 2 del array (2 * 0 + 2 = 2).
-   El hijo izquierdo de 20 (40) se almacena en la posición 3 del array (2 * 1 + 1 = 3).
-   El hijo derecho de 20 (50) se almacena en la posición 4 del array (2 * 1 + 2 = 4).

De esta manera, podemos representar de manera eficiente un heap binario utilizando un array y acceder a los elementos relacionados (padre, hijo izquierdo, hijo derecho) mediante simples cálculos de índice.

## Ventajas

1.  **Eficiencia en el uso de memoria**: Al utilizar un array para representar un heap, no es necesario almacenar punteros explícitos para los nodos hijos y padres, lo que ahorra memoria. La relación padre-hijo se mantiene a través de cálculos de índices basados en la posición del elemento en el array.

2.  **Acceso rápido a elementos padres e hijos**: En un heap binario implementado con un array, dado el índice `i` de un elemento, es fácil calcular los índices de su padre, hijo izquierdo y hijo derecho mediante fórmulas simples.

3.  **Fácil de implementar**: La implementación de un heap utilizando un array es simple y directa. La mayoría de las operaciones en un heap, como insertar y eliminar elementos, se pueden realizar mediante manipulaciones de índices en lugar de modificar punteros explícitos.

## Desventajas

1.  **Tamaño fijo**: En el caso de un array de tamaño fijo, si el heap crece y supera la capacidad del array, es necesario re-dimensionar el array, lo que implica copiar los elementos a un nuevo array más grande. Esto puede ser costoso en términos de tiempo y memoria, especialmente si el re-dimensionamiento ocurre con frecuencia.

2.  **No es óptimo para buscar o eliminar elementos arbitrarios**: Como mencioné anteriormente, un heap no es la estructura de datos más adecuada para buscar o eliminar elementos específicos que no sean la raíz, independientemente de si está implementado utilizando un array o no. Las búsquedas y eliminaciones de elementos específicos pueden ser ineficientes en términos de tiempo.

## Código

```cpp
#include <iostream>

template <typename T>
class BinaryHeap {
public:
    BinaryHeap(int capacity) : size(0), capacity(capacity) {
        heap = new T[capacity + 1];
    }

    ~BinaryHeap() {
        delete[] heap;
    }

    // Insertar un elemento en el heap
    void insert(T value) {
        if (size == capacity) {
            std::cout << "Heap is full" << std::endl;
            return;
        }
        size++;
        heap[size] = value;
        swim(size);
    }

    // Eliminar el elemento máximo
    T removeMax() {
        if (isEmpty()) {
            std::cout << "Heap is empty" << std::endl;
            return T();
        }
        T maxValue = heap[1];
        swap(1, size);
        size--;
        sink(1);
        return maxValue;
    }

    // Verificar si el heap está vacío
    bool isEmpty() {
        return size == 0;
    }

private:
    T* heap;
    int size;
    int capacity;

    // Mantener la propiedad de max-heap
    void swim(int index) {
        while (index > 1 && heap[index / 2] < heap[index]) {
            swap(index, index / 2);
            index = index / 2;
        }
    }

    void sink(int index) {
        while (2 * index <= size) {
            int j = 2 * index;
            if (j < size && heap[j] < heap[j + 1]) j++;
            if (heap[index] >= heap[j]) break;
            swap(index, j);
            index = j;
        }
    }

    // Intercambiar dos elementos en el heap
    void swap(int i, int j) {
        T temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }
};
```

Este código en C++ define una clase `BinaryHeap` que implementa un max-heap utilizando un array. Un max-heap es una estructura de datos que mantiene el orden parcial de sus elementos de tal manera que el elemento máximo siempre está en la raíz. A continuación se detallan las partes clave del código:

1.  La clase `BinaryHeap` es una plantilla que admite un tipo de datos genérico `T`. Esto permite que el heap almacene elementos de cualquier tipo que se pueda comparar (que admita operadores `<`, `>` y `==`).
   
> [!warning]
> Es importante que el tipo `T` implemente estas operaciones para ser usando dentro del heap. Tipos primitivos cono `int` ya lo tienen en implementado.

2.  La función constructora `BinaryHeap(int capacity)` inicializa el heap con una capacidad dada, crea un array dinámico de tamaño `capacity + 1`, y establece el tamaño del heap en 0. El array se crea con un tamaño de `capacity + 1` porque el primer elemento del array (índice 0) se deja sin usar para simplificar los cálculos de índice en las funciones `swim` y `sink`.

3.  La función destructora `~BinaryHeap()` libera la memoria utilizada por el array dinámico.

4.  La función `insert(T value)` inserta un nuevo elemento en el heap. Si el heap está lleno, se muestra un mensaje de error. De lo contrario, incrementa el tamaño del heap, agrega el elemento al final del array, y lo "flota" hacia arriba (swim) para mantener la propiedad de max-heap.

5.  La función `removeMax()` elimina y devuelve el elemento máximo del heap (la raíz). Si el heap está vacío, se muestra un mensaje de error. De lo contrario, intercambia el último elemento con la raíz, reduce el tamaño del heap en 1 y "hunde" (sink) el elemento en la posición de la raíz para mantener la propiedad de max-heap.

6.  La función `isEmpty()` devuelve verdadero si el heap está vacío (tamaño 0) y falso de lo contrario.

7.  Las funciones privadas `swim(int index)` y `sink(int index)` se utilizan para mantener la propiedad de max-heap al flotar hacia arriba (swim) y hundir (sink) elementos en el heap.

8.  La función privada `swap(int i, int j)` intercambia dos elementos en el array del heap.


En resumen, este código define una clase `BinaryHeap` que implementa un max-heap utilizando un array. La clase admite operaciones básicas como insertar, eliminar el elemento máximo y verificar si el heap está vacío.

# Heap + Cola de prioridad

La relación entre un heap y una [[Cola de prioridad]] es que un heap es una implementación común y eficiente de una cola de prioridades. Un heap puede ser utilizado para implementar las operaciones básicas de una cola de prioridades, como insertar elementos, eliminar el elemento prioritario y verificar si la cola de prioridades está vacía, todo ello en tiempo logarítmico (O(log n)). Esto hace que un heap sea una opción popular para implementar colas de prioridades en aplicaciones prácticas.