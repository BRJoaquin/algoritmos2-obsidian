---
tag: TAD
---

  
Una cola de prioridad es un tipo abstracto de datos (TAD) que se utiliza para gestionar un conjunto de elementos con ciertas prioridades asociadas. En una cola de prioridad, los elementos se insertan en cualquier orden, pero se eliminan según su nivel de prioridad. El elemento con la prioridad más alta es el primero en ser eliminado. Si varios elementos tienen la misma prioridad, se atienden según el orden en que fueron agregados a la cola.

Las colas de prioridad son útiles en diversas aplicaciones, como la planificación de procesos en sistemas operativos, algoritmos de ruta más corta en gráficos, compresión de datos y simulaciones de eventos discretos, entre otros.

Existen varias formas de implementar una cola de prioridad, algunas de las más comunes son:

1.  Lista enlazada o array ordenado: Se insertan los elementos en la estructura de datos **de manera ordenada**, según su prioridad. La inserción puede ser lenta ($O(n)$) pero la eliminación del elemento con mayor prioridad es rápida ($O(1)$).

2.  [[Lista simplemente encadenada]] o array no ordenado: Los elementos se insertan **sin ningún orden específico**, lo que resulta en una inserción rápida ($O(1)$). Sin embargo, eliminar el elemento de mayor prioridad puede ser lento ($O(n)$), ya que se debe buscar en toda la estructura.

3.  Montículo ([[Heap]]): Es una estructura de datos basada en un árbol binario, que permite la inserción y eliminación de elementos con complejidad $O(log (n))$ (peor caso). El montículo puede ser de tipo mínimo (min-heap) o máximo (max-heap), dependiendo de si se quiere obtener el elemento de menor o mayor prioridad, respectivamente. **Los montículos son una de las implementaciones más eficientes y comunes de colas de prioridad**.

En general, la elección de la implementación de una cola de prioridad dependerá de los requisitos de rendimiento y las operaciones específicas que se realicen con mayor frecuencia en la aplicación donde se utilizará.