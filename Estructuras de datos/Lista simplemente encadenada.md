
# Intro

Una lista simplemente enlazada es una [[Estructura de datos]] lineal en la que cada elemento, llamado nodo, está compuesto por un valor y un puntero que apunta al siguiente nodo en la lista. El primer nodo se llama cabeza o inicio de la lista, y el último nodo apunta a NULL.

Las operaciones básicas en una lista simplemente enlazada son la inserción, eliminación y búsqueda de elementos. Para insertar un nuevo nodo, se crea un nodo con el valor deseado y se ajustan los punteros para que el nuevo nodo apunte al siguiente nodo y el nodo anterior apunte al nuevo nodo. Para eliminar un nodo, se ajustan los punteros del nodo anterior y siguiente para que apunten entre sí y se libera la memoria ocupada por el nodo eliminado. Para buscar un elemento, se recorre la lista desde el primer nodo hasta encontrar el valor deseado o hasta llegar al final de la lista.

Las listas simplemente enlazadas son eficientes para la inserción y eliminación de elementos en la cabeza de la lista, ya que solo se requiere actualizar el puntero de la cabeza. Sin embargo, para acceder a un elemento en una posición arbitraria de la lista se requiere recorrer la lista desde el principio, lo que puede ser ineficiente en listas grandes.

# Implementacion

## Nodo Lista

```cpp
template <typename T>
struct ListNode {
	// Store de value
    T val;
    // Pointer to the next node
    ListNode<T>* next;

	// Constructor
    ListNode(T x) : val(x), next(nullptr) {}
};
```

Esta plantilla define un nodo de lista enlazada con un miembro `val` de tipo `T` para contener el valor del nodo, y un puntero `next` de tipo `NodoLista<T>*` para apuntar al siguiente nodo en la lista. El constructor toma un valor de tipo `T` e inicializa el miembro `val` a ese valor, y establece el puntero `next` en `nullptr`.

El uso de plantillas nos permite definir un nodo de lista enlazada que puede contener cualquier tipo de valor, no solo un tipo específico. Por ejemplo, podríamos crear una lista enlazada de enteros utilizando `NodoLista<int>`, o una lista enlazada de cadenas utilizando `NodoLista<std::string>`.

## Lista simplemente encandeada/enlazada

```cpp
#include <iostream>

template <typename T>
class LinkedList {
private:
    ListNode<T>* head;
    int length;

public:
    LinkedList() : head(nullptr), length(0) {}

    ~LinkedList() {
        ListNode<T>* current = head;
        while (current != nullptr) {
            ListNode<T>* next = current->next;
            delete current;
            current = next;
        }
    }

    void addToStart(T x) {
        ListNode<T>* new_node = new ListNode<T>(x);
        new_node->next = head;
        head = new_node;
        length++;
    }

    void addToEnd(T x) {
        ListNode<T>* new_node = new ListNode<T>(x);
        if (head == nullptr) {
            head = new_node;
        } else {
            ListNode<T>* current = head;
            while (current->next != nullptr) {
                current = current->next;
            }
            current->next = new_node;
        }
        length++;
    }

    void remove(T x) {
        ListNode<T>* current = head;
        ListNode<T>* previous = nullptr;
        while (current != nullptr) {
            if (current->val == x) {
                if (previous == nullptr) {
                    head = current->next;
                } else {
                    previous->next = current->next;
                }
                delete current;
                length--;
                return;
            }
            previous = current;
            current = current->next;
        }
    }

    void print() {
        ListNode<T>* current = head;
        while (current != nullptr) {
            std::cout << current->val << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    int size() {
        return length;
    }
};
```

Esta implementación define una clase de lista enlazada llamada `LinkedList` que utiliza la estructura `ListNode` como su tipo de nodo. La clase tiene miembros privados para el puntero de la cabeza y la longitud de la lista, y métodos públicos para agregar nodos al inicio o al final de la lista, eliminar nodos por valor, imprimir la lista y obtener su tamaño.

El método `addToStart` crea un nuevo nodo con el valor dado, establece su puntero `next` en la cabeza actual de la lista y establece el puntero de la cabeza en el nuevo nodo. El método `addToEnd` crea un nuevo nodo con el valor dado y lo agrega al final de la lista recorriendo la lista hasta encontrar el último nodo y estableciendo su puntero `next` en el nuevo nodo.

El método `remove` recorre la lista buscando un nodo con el valor dado, y lo elimina de la lista ajustando su puntero `next` en el nodo anterior o en el puntero de la cabeza, dependiendo de si el nodo a eliminar es la cabeza de la lista o no.

El método `print` recorre la lista e imprime el valor de cada nodo, separado por espacios. El método `size` simplemente devuelve la longitud de la lista.

# Ordenes

Aquí están las complejidades de tiempo de las operaciones comunes en una lista enlazada:

-  **Acceder a un elemento en una posición arbitraria**: O(n), donde n es la longitud de la lista, ya que puede ser necesario recorrer la lista desde el principio para encontrar el elemento deseado.
  
-  **Insertar un elemento al inicio de la lista**: O(1), ya que solo se necesita ajustar el puntero de la cabeza.
  
-  **Insertar un elemento al final de la lista**: O(n), donde n es la longitud de la lista, ya que se debe recorrer la lista para encontrar el último nodo y agregar el nuevo nodo como su siguiente.
  
-  **Eliminar un elemento en una posición arbitraria**: O(n), donde n es la longitud de la lista, ya que puede ser necesario recorrer la lista desde el principio para encontrar el elemento deseado y ajustar los punteros.
  
-  **Eliminar el primer elemento de la lista**: O(1), ya que solo se necesita ajustar el puntero de la cabeza.
  
-  **Eliminar el último elemento de la lista**: O(n), donde n es la longitud de la lista, ya que se debe recorrer la lista para encontrar el penúltimo nodo y ajustar su puntero siguiente a NULL.
  
-  **Calcular la longitud de la lista**: O(1), si se mantiene un contador de longitud en la lista.
  
-  **Recorrer toda la lista para realizar una operación en cada elemento**: O(n), donde n es la longitud de la lista, ya que se debe recorrer cada nodo una vez.

# Variaciones / mejoras

Hay varias maneras de mejorar los tiempos de ejecución de las operaciones en una lista enlazada. Aquí hay algunas técnicas comunes que se utilizan para mejorar la eficiencia de las operaciones:

-  **Mantener un puntero al último nodo**: Si se mantiene un puntero al último nodo de la lista, se puede insertar un elemento al final de la lista en tiempo O(1) en lugar de O(n), ya que no es necesario recorrer la lista completa para encontrar el último nodo.

-  **Implementar una** [[Lista doblemente encadenada]]: En una lista doblemente enlazada, cada nodo tiene un puntero al nodo anterior y al siguiente. Esto permite eliminar un elemento en una posición arbitraria en tiempo O(1), en lugar de O(n), ya que no es necesario buscar el nodo anterior.

-  **Usar una lista circular**: En una lista circular, el último nodo de la lista apunta al primer nodo en lugar de a NULL. Esto permite un acceso más rápido al primer nodo de la lista y hace que algunas operaciones sean más eficientes.

# Utilidad / usos

La estructura de datos de lista enlazada es útil en situaciones donde necesitamos una colección de elementos ordenados que deben ser insertados o eliminados de manera eficiente.

A diferencia de un arreglo, donde los elementos están almacenados en una ubicación contigua de memoria, en una lista enlazada cada elemento está enlazado al siguiente mediante un puntero, lo que permite una inserción y eliminación eficiente de elementos en cualquier posición de la lista.

Además, las listas enlazadas no tienen un tamaño fijo, por lo que pueden crecer o disminuir según sea necesario. Esto las hace útiles en situaciones donde el tamaño de la colección no es conocido de antemano o puede cambiar dinámicamente.

Las listas enlazadas también pueden ser usadas para implementar TADs, como [[Cola]], [[Pila]], Arbol N y [[Grafo]] ([[Grafo#Lista de adyacencia]]), ya que proporcionan una forma eficiente de almacenar y manipular elementos.


# Mas información

- https://www.geeksforgeeks.org/what-is-linked-list/