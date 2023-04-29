---
tag: TAD
---

  
Una cola de prioridad es un tipo abstracto de datos (TAD) que se utiliza para gestionar un conjunto de elementos con ciertas prioridades asociadas. En una cola de prioridad, los elementos se insertan en cualquier orden, pero se eliminan según su nivel de prioridad. El elemento con la prioridad más alta es el primero en ser eliminado. Si varios elementos tienen la misma prioridad, se atienden según el orden en que fueron agregados a la cola.

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

