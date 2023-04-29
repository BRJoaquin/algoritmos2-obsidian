---
tag: TAD
---

Una cola de prioridad es un [[Tipo Abstracto de Dato (TAD)]] que se utiliza para gestionar un conjunto de elementos con ciertas prioridades asociadas. En una cola de prioridad, los elementos se insertan en cualquier orden, pero se eliminan según su nivel de prioridad. El elemento con la prioridad más alta es el primero en ser eliminado. Si varios elementos tienen la misma prioridad, se atienden según el orden en que fueron agregados a la cola.

Las colas de prioridad son útiles en diversas aplicaciones, como la planificación de procesos en sistemas operativos, algoritmos de ruta más corta en gráficos, compresión de datos y simulaciones de eventos discretos, entre otros.

Existen varias formas de implementar una cola de prioridad, algunas de las más comunes son:

1.  Lista enlazada o array ordenado: Se insertan los elementos en la estructura de datos **de manera ordenada**, según su prioridad. La inserción puede ser lenta ($O(n)$) pero la eliminación del elemento con mayor prioridad es rápida ($O(1)$).

2.  [[Lista simplemente encadenada]] o array no ordenado: Los elementos se insertan **sin ningún orden específico**, lo que resulta en una inserción rápida ($O(1)$). Sin embargo, eliminar el elemento de mayor prioridad puede ser lento ($O(n)$), ya que se debe buscar en toda la estructura.

3.  Montículo ([[Heap]]): Es una estructura de datos basada en un árbol binario, que permite la inserción y eliminación de elementos con complejidad $O(log (n))$ (peor caso). El montículo puede ser de tipo mínimo (min-heap) o máximo (max-heap), dependiendo de si se quiere obtener el elemento de menor o mayor prioridad, respectivamente. **Los montículos son una de las implementaciones más eficientes y comunes de colas de prioridad**.

# Definición

```cpp
#ifndef PRIORITY_QUEUE_H
#define PRIORITY_QUEUE_H

template<typename T>
class PriorityQueue {
public:
    // Constructor por defecto
    PriorityQueue() {}

    // Destructor virtual para asegurar la eliminación correcta de objetos derivados
    virtual ~PriorityQueue() {}

    // Pre-condición: ninguna
    // Post-condición: devuelve verdadero si la cola de prioridad está vacía, falso en caso contrario
    virtual bool empty() const = 0;

    // Pre-condición: ninguna
    // Post-condición: devuelve la cantidad de elementos en la cola de prioridad
    virtual int size() const = 0;

    // Pre-condición: la cola de prioridad no debe estar vacía
    // Post-condición: devuelve el elemento con la mayor prioridad
    virtual const T& top() const = 0;

    // Pre-condición: ninguna
    // Post-condición: inserta el elemento en la cola de prioridad según su prioridad
    virtual void push(const T& value, int priority) = 0;

    // Pre-condición: la cola de prioridad no debe estar vacía
    // Post-condición: elimina el elemento con la mayor prioridad
    virtual void pop() = 0;
};

#endif // PRIORITY_QUEUE_H
```

# Cola de prioridad extendida

Una cola de prioridad extendida es una variante de la cola de prioridad básica que incluye dos métodos adicionales para aumentar su funcionalidad: `changePriority`,  `delete` y  `exists`. Estos métodos permiten modificar la prioridad de un elemento en la cola y eliminar un elemento específico, respectivamente.

```cpp
#ifndef EXTENDED_PRIORITY_QUEUE_H
#define EXTENDED_PRIORITY_QUEUE_H

#include "PriorityQueue.h"

template<typename T>
class ExtendedPriorityQueue : public PriorityQueue<T> {
public:
    // Constructor por defecto
    ExtendedPriorityQueue() {}

    // Destructor virtual
    virtual ~ExtendedPriorityQueue() {}

    // Pre-condición: el elemento debe estar en la cola de prioridad
    // Post-condición: cambia la prioridad del elemento en la cola de prioridad
    virtual void changePriority(const T& value, int newPriority) = 0;

    // Pre-condición: el elemento debe estar en la cola de prioridad
    // Post-condición: elimina el elemento específico de la cola de prioridad
    virtual void deleteElement(const T& value) = 0;

	// Pre-condición: ninguna 
	// Post-condición: devuelve verdadero si el elemento existe en la cola de prioridad, falso en caso contrario 
	virtual bool exists(const T& value) const = 0;
};

#endif // EXTENDED_PRIORITY_QUEUE_H
```

## Implementación con heap

Cuando se implementa una **cola de prioridad extendida** utilizando únicamente un [[Heap]] (montículo), algunos de los métodos adicionales, como `changePriority`, `deleteElement` y `exists`, pueden tener una complejidad de tiempo peor que con otras estructuras de datos.

**En un heap, encontrar un elemento específico tiene una complejidad de tiempo $O(n)$ en el peor caso, ya que puede ser necesario recorrer todo el heap.** Como resultado, las operaciones `changePriority` y `deleteElement` también tendrán una complejidad de tiempo $O(n)$ en el peor caso, dado que primero se debe encontrar el elemento antes de realizar las operaciones de cambio de prioridad o eliminación.

Una posible solución para mejorar el rendimiento de estas operaciones es utilizar una estructura de datos auxiliar junto con el heap, como una [[Tabla de hash]]. **La tabla de hash puede almacenar la ubicación de los elementos en el heap,** lo que permite encontrar y acceder a un elemento específico en tiempo constante promedio $O(1)$ (caso promedio). Al combinar el heap y la tabla de hash, las operaciones `changePriority`, `deleteElement` y `exists` pueden volverse más eficientes.