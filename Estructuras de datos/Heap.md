---
tag: estructura_de_datos
---

# Intro

Un heap binario es una [[Estructura de datos]] de tipo árbol binario que cumple con dos propiedades fundamentales:

1.  **Propiedad estructural**: Es un árbol binario completo, excepto quizás en el último nivel, donde los nodos pueden no estar presentes a la derecha. Esto significa que todos los niveles del árbol, excepto posiblemente el último, están completamente llenos de nodos, y los nodos en el último nivel están lo más a la izquierda posible.

![[Pasted image 20230401085607.jpg|700]]


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





# Contras

