---
tag: estructura_de_datos
---

Una lista doblemente encadenada es una estructura de datos lineal en la que cada elemento, o nodo, contiene un valor y dos punteros que apuntan a los nodos vecinos. Cada nodo tiene un puntero que apunta al nodo anterior y otro que apunta al nodo siguiente.

Las operaciones básicas que se pueden realizar en una lista doblemente encadenada incluyen la inserción y eliminación de elementos en cualquier posición, así como la búsqueda y acceso a los elementos. Para insertar un elemento en una lista doblemente encadenada, se necesita ajustar los punteros de los nodos vecinos para apuntar al nuevo nodo. Para eliminar un elemento, se necesitan ajustar los punteros de los nodos vecinos para saltar el nodo que se está eliminando.

La ventaja de usar una lista doblemente encadenada en comparación con una [[Lista simplemente encadenada]] es que se puede iterar en ambas direcciones, lo que puede ser útil en ciertas situaciones. Sin embargo, una lista doblemente encadenada utiliza más memoria que una lista simplemente encadenada, ya que cada nodo necesita un puntero adicional para el nodo anterior.

# Implementacion

## Nodo

```cpp
template <typename T>
class Node {
public:
    T data;
    Node* next;
    Node* prev;

    Node(T value) {
        data = value;
        next = nullptr;
        prev = nullptr;
    }
};
```

```cpp
template <typename T>
class DoublyLinkedList {
private:
    Node<T>* head;
    Node<T>* tail;
    int size;

public:
    DoublyLinkedList() {
        head = nullptr;
        tail = nullptr;
        size = 0;
    }

    void push_back(T value) {
        Node<T>* newNode = new Node<T>(value);
        if (head == nullptr) {
            head = newNode;
            tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        size++;
    }

    void push_front(T value) {
        Node<T>* newNode = new Node<T>(value);
        if (head == nullptr) {
            head = newNode;
            tail = newNode;
        } else {
            head->prev = newNode;
            newNode->next = head;
            head = newNode;
        }
        size++;
    }

    void insert(T value, int pos) {
        if (pos < 0 || pos > size) {
            cout << "Invalid position\n";
            return;
        }
        if (pos == 0) {
            push_front(value);
            return;
        }
        if (pos == size) {
            push_back(value);
            return;
        }
        Node<T>* newNode = new Node<T>(value);
        Node<T>* curr = head;
        for (int i = 0; i < pos - 1; i++) {
            curr = curr->next;
        }
        newNode->prev = curr;
        newNode->next = curr->next;
        curr->next->prev = newNode;
        curr->next = newNode;
        size++;
    }

    void pop_back() {
        if (head == nullptr) {
            cout << "List is empty\n";
            return;
        }
        if (head == tail) {
            delete head;
            head = nullptr;
            tail = nullptr;
        } else {
            Node<T>* temp = tail;
            tail = tail->prev;
            tail->next = nullptr;
            delete temp;
        }
        size--;
    }

    void pop_front() {
        if (head == nullptr) {
            cout << "List is empty\n";
            return;
        }
        if (head == tail) {
            delete head;
            head = nullptr;
            tail = nullptr;
        } else {
            Node<T>* temp = head;
            head = head->next;
            head->prev = nullptr;
            delete temp;
        }
        size--;
    }

    void remove(int pos) {
        if (pos < 0 || pos >= size) {
            cout << "Invalid position\n";
            return;
        }
        if (pos == 0) {
            pop_front();
            return;
        }
        if (pos == size - 1) {
            pop_back();
            return;
        }
        Node<T>* curr = head;
        for (int i = 0; i < pos; i++) {
            curr = curr->next;
        }
        curr->prev->next = curr->next;
        curr->next->prev = curr->prev; 
        delete curr; 
        size--; 
    }
}
```

Este código implementa una lista doblemente enlazada en C++ utilizando plantillas (`template`) para hacer que la lista sea genérica y poder trabajar con cualquier tipo de dato.

La clase `DoublyLinkedList` tiene tres variables privadas: `head` y `tail` son punteros a los nodos de la cabeza y de la cola de la lista, respectivamente, y `size` es el tamaño de la lista. Los métodos públicos de la clase permiten agregar elementos al final y al principio de la lista (`push_back` y `push_front`, respectivamente), insertar elementos en cualquier posición de la lista (`insert`), eliminar elementos del final y del principio de la lista (`pop_back` y `pop_front`, respectivamente), eliminar elementos de cualquier posición de la lista (`remove`) y imprimir los elementos de la lista (`print`).

En cuanto a los métodos de la clase, `push_back` y `push_front` crean un nuevo nodo con el valor especificado, lo enlazan al final o al principio de la lista, respectivamente, y actualizan los punteros de cabeza y cola, además del tamaño de la lista. `insert` inserta un nuevo nodo en la posición especificada, lo enlaza con los nodos vecinos y actualiza los punteros y tamaño de la lista.

`pop_back` y `pop_front` eliminan el nodo correspondiente y actualizan los punteros y tamaño de la lista. En el caso de `remove`, el método busca el nodo en la posición especificada, lo elimina, enlaza los nodos vecinos y actualiza el tamaño de la lista.

## Ordenes 

-   `DoublyLinkedList()`: O(1)
-   `void push_back(T value)`: O(1)
-   `void push_front(T value)`: O(1)
-   `void insert(T value, int pos)`: O(n)
-   `void pop_back()`: O(1)
-   `void pop_front()`: O(1)
-   `void remove(int pos)`: O(n)

En general, los métodos de inserción y eliminación tienen una complejidad temporal de O(n) en el peor caso, ya que en algunas situaciones es necesario recorrer la lista para encontrar la posición correcta. Por otro lado, los métodos de acceso (`push_back`, `push_front`, `pop_back`, `pop_front`) tienen una complejidad de O(1) en el peor caso, ya que no necesitan recorrer la lista para realizar la operación.

# Lista simple encadenada vs doblemente encadenada

| Lista simplemente enlazada | Lista doblemente enlazada |
| ------------------------- | -------------------------- |
| Cada nodo solo tiene un puntero al siguiente nodo | Cada nodo tiene un puntero al siguiente y al anterior nodo |
| El recorrido inverso es difícil de implementar | El recorrido inverso es fácil de implementar |
| Eliminar un nodo requiere recorrer la lista para encontrar el nodo anterior | Eliminar un nodo es más eficiente porque se pueden actualizar los punteros del nodo anterior y siguiente |
| Inserción en la cabeza de la lista es O(1) | Inserción en la cabeza de la lista es O(1) |
| Inserción en la cola de la lista es O(n) | Inserción en la cola de la lista es O(1) |
| Acceso a un elemento es O(n) en el peor caso | Acceso a un elemento es O(n) en el peor caso |
| Requiere menos memoria que una lista doblemente enlazada | Requiere más memoria que una lista simplemente enlazada debido a los punteros adicionales en cada nodo |


La elección de usar una lista simplemente enlazada o una lista doblemente enlazada dependerá de las necesidades específicas del problema que estés resolviendo. Aquí te proporciono algunas consideraciones que pueden ayudarte a decidir qué tipo de lista utilizar:

-   La lista simplemente enlazada puede ser más adecuada si se necesita una estructura de datos más ligera y se tiene un uso más limitado de la operación de eliminación de nodos, ya que en esta estructura, la eliminación de nodos requiere recorrer la lista para encontrar el nodo anterior.

-   La lista doblemente enlazada puede ser más adecuada si se necesita la capacidad de recorrer la lista en ambas direcciones, o si la operación de eliminación de nodos es una operación crítica en el problema que estás resolviendo. En esta estructura, la eliminación de nodos es más eficiente, ya que se pueden actualizar los punteros del nodo anterior y siguiente para eliminar el nodo.

-   También es importante tener en cuenta la cantidad de memoria que se tiene disponible y el tamaño de los datos que se están manejando. La lista doblemente enlazada requiere más memoria que la lista simplemente enlazada debido a los punteros adicionales en cada nodo, lo que puede ser importante si se tiene una cantidad limitada de memoria disponible.

En general, si necesitas una estructura de datos más ligera y la eliminación de nodos no es una operación crítica en tu problema, una lista simplemente enlazada podría ser la mejor opción. Si necesitas la capacidad de recorrer la lista en ambas direcciones o la eliminación de nodos es una operación crítica en tu problema, una lista doblemente enlazada podría ser la mejor opción.