---
tag: TAD
---

# Intro

La Cola es un [[Tipo Abstracto de Dato (TAD)]] en la que los elementos se insertan y eliminan siguiendo una regla conocida como "primero en entrar, primero en salir" (FIFO, por sus siglas en inglés). Es decir, el primer elemento que se inserta es el primero en ser eliminado y los elementos que se insertan después se van colocando detrás en la cola.

La cola tiene dos operaciones básicas: enqueue (encolar) y dequeue (desencolar). La operación enqueue agrega un elemento al final de la cola, mientras que la operación dequeue elimina el elemento que se encuentra al principio de la cola y devuelve su valor.

Además de estas operaciones básicas, una cola puede tener otras operaciones complementarias, como la obtención del elemento que está al principio de la cola sin eliminarlo (peek), o la comprobación del tamaño de la cola (size).

Una de las aplicaciones más comunes de las colas es la implementación de procesos en un sistema operativo. Los procesos se colocan en una cola y se ejecutan de acuerdo con el principio FIFO. También se utilizan en la gestión de recursos compartidos, como en una cola de impresión, donde los trabajos de impresión se procesan en el orden en que se reciben.

En resumen, una cola es una estructura de datos que permite agregar elementos al final y eliminar elementos del principio siguiendo una regla de ordenamiento conocida como FIFO. Es una estructura de datos simple pero muy útil para una amplia gama de aplicaciones en la informática y otras áreas.

# Definicion

```cpp
template<typename T>
class Queue {
public:
    // Description: Inserts an element at the back of the queue.
    // Preconditions: None.
    // Postconditions: Adds 'value' to the back of the queue.
    void enqueue(const T& value);

    // Description: Removes and returns the element at the front of the queue.
    // Preconditions: The queue is not empty.
    // Postconditions: Removes and returns the element at the front of the queue. 
    T dequeue();

    // Description: Returns the element at the front of the queue without removing it.
    // Preconditions: The queue is not empty.
    // Postconditions: Returns the element at the front of the queue.
    T peek() const;

    // Description: Returns true if the queue is empty, false otherwise.
    // Preconditions: None.
    // Postconditions: Returns true if the queue is empty, false otherwise.
    bool isEmpty() const;

    // Description: Returns the number of elements in the queue.
    // Preconditions: None.
    // Postconditions: Returns the number of elements in the queue.
    int size() const;
};

```

## Enqueue / encolar 

El método `enqueue` es una de las operaciones fundamentales en la estructura de datos de cola. La función de este método es agregar un elemento al final de la cola, siguiendo el principio de "primero en entrar, primero en salir" (FIFO).

En la implementación de una cola usando una lista enlazada, el método `enqueue` agrega un nuevo nodo al final de la lista. Si la cola está vacía, el nuevo nodo se convierte en el primer elemento de la cola, y tanto el puntero al frente como al final de la cola apuntan a él. Si la cola ya tiene elementos, se agrega el nuevo nodo al final de la lista y se actualiza el puntero al final de la cola.

## Dequeue / desencolar

El método `dequeue` es otra de las operaciones fundamentales en la estructura de datos de cola. La función de este método es eliminar el elemento que se encuentra al frente de la cola y devolver su valor, siguiendo el principio de "primero en entrar, primero en salir" (FIFO).

En la implementación de una cola usando una lista enlazada, el método `dequeue` elimina el primer nodo de la lista y devuelve el valor de su elemento. Si la cola está vacía, el método `dequeue` lanza una excepción, ya que no hay ningún elemento que se pueda eliminar.

El método `dequeue` tiene una precondición muy importante: la cola no debe estar vacía. Si la cola está vacía, el método `dequeue` no puede eliminar ningún elemento y, por lo tanto, lanzará una excepción para indicar que la operación no se pudo realizar.

## Peek / tope

El método `dequeue` es otra de las operaciones fundamentales en la estructura de datos de cola. La función de este método es eliminar el elemento que se encuentra al frente de la cola y devolver su valor, siguiendo el principio de "primero en entrar, primero en salir" (FIFO).

En la implementación de una cola usando una lista enlazada, el método `dequeue` elimina el primer nodo de la lista y devuelve el valor de su elemento. Si la cola está vacía, el método `dequeue` lanza una excepción, ya que no hay ningún elemento que se pueda eliminar.

El método `peek` tiene una precondición muy importante: la cola no debe estar vacía. Si la cola está vacía, el método `peek` no puede devolver ningún valor y, por lo tanto, lanzará una excepción para indicar que la operación no se pudo realizar.

La postcondición de `peek` es que se devuelve el valor del elemento al frente de la cola, sin modificar la cola en sí misma. La cola permanece en el mismo estado en el que estaba antes de llamar a `peek`.

## isEmpty / esVacia

El método `isEmpty` es una operación común en la estructura de datos de cola. La función de este método es comprobar si la cola está vacía, es decir, si no hay elementos en la cola para eliminar.

# Implementacion

## Lista enlazada

Hay varias formas de implementar una lista en C++, pero una de las más comunes es mediante el uso de una [[Lista simplemente encadenada]]. Una lista enlazada es una [[Estructura de datos]] en la que cada elemento, o nodo, contiene un valor y un puntero al siguiente nodo en la lista. El primer nodo de la lista se conoce como la cabeza, y el último nodo se llama la cola.

Para crear una lista enlazada, se puede definir una clase o una estructura que represente un nodo en la lista, y que contenga un miembro para almacenar el valor del nodo y otro miembro que sea un puntero al siguiente nodo en la lista.

Luego, se puede definir otra clase o estructura para representar la lista en sí, que contenga punteros a los nodos de la cabeza y de la cola, así como un contador para realizar un seguimiento del número de elementos en la lista.

Una vez que se han definido las clases y estructuras necesarias, se pueden implementar varios métodos para trabajar con la lista, como la inserción de elementos en la cabeza o en la cola de la lista, la eliminación de elementos de la lista, la búsqueda de elementos en la lista y la obtención del tamaño de la lista.

En resumen, la implementación de una lista puede variar dependiendo de la estructura de datos que se utilice, pero una de las formas más comunes de implementar una lista es mediante el uso de una lista enlazada, que consta de nodos que contienen un valor y un puntero al siguiente nodo en la lista, y una clase o estructura que representa la lista en sí, que contiene punteros a los nodos de la cabeza y de la cola, así como un contador para realizar un seguimiento del número de elementos en la lista.

```cpp
template<typename T>
class Queue {
private:
    struct Node {
        T value;
        Node* next;
        Node(const T& v, Node* n = nullptr) : value(v), next(n) {}
    };
    Node* head;
    Node* tail;
    int size;
public:
    Queue() : head(nullptr), tail(nullptr), size(0) {}

    ~Queue() {
        while(head) {
            Node* current = head;
            head = head->next;
            delete current;
        }
    }

    bool isEmpty() const {
        return size == 0;
    }

    int length() const {
        return size;
    }

    void enqueue(const T& value) {
        Node* newNode = new Node(value);
        if(isEmpty()) {
            head = newNode;
        } else {
            tail->next = newNode;
        }
        tail = newNode;
        size++;
    }

    T dequeue() {
        if(isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        Node* temp = head;
        T value = temp->value;
        head = head->next;
        delete temp;
        if(head == nullptr) {
            tail = nullptr;
        }
        size--;
        return value;
    }

    T peek() const {
        if(isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        return head->value;
    }
};
```

En esta implementación, cada elemento de la cola es un nodo en la lista enlazada. El puntero `head` apunta al primer nodo de la lista (el elemento al frente de la cola), y el puntero `tail` apunta al último nodo de la lista (el elemento al final de la cola).

El método `enqueue` agrega un nuevo nodo al final de la lista, actualizando el puntero `tail`. El método `dequeue` elimina el primer nodo de la lista (el elemento al frente de la cola) y devuelve su valor, actualizando el puntero `head`. El método `peek` devuelve el valor del primer nodo de la lista sin eliminarlo. El método `isEmpty` verifica si la cola está vacía.

En resumen, esta implementación de cola usando una lista enlazada en C++ proporciona una forma eficiente y elegante de implementar las operaciones de cola básicas, como `enqueue`, `dequeue`, `peek`, y `isEmpty`.

### Ordenes

-   `enqueue`: O(1) - Agrega un nuevo elemento al final de la cola enlazada. Ya que siempre se agrega un elemento al final de la cola, el tiempo de ejecución no depende del tamaño actual de la cola.

-   `dequeue`: O(1) - Elimina el primer elemento de la cola enlazada. Como el primer elemento de la cola es siempre el que se elimina, el tiempo de ejecución no depende del tamaño actual de la cola.

-   `peek`: O(1) - Devuelve el valor del primer elemento de la cola enlazada sin eliminarlo. Esta operación es constante ya que solo se devuelve el valor del primer elemento.

-   `isEmpty`: O(1) - Verifica si la cola enlazada está vacía. Esta operación es constante ya que solo se comprueba si el tamaño de la cola es cero.

-   `length`: O(1) - Devuelve la longitud (tamaño) de la cola enlazada. Esta operación es constante ya que el tamaño de la cola se almacena como un miembro de la clase.

## Array

```cpp
template<typename T>
class Queue {
private:
    T* arr;
    int head;
    int tail;
    int capacity;
    int size;
public:
    Queue(int cap) : head(0), tail(0), capacity(cap), size(0) {
        arr = new T[capacity];
    }

    ~Queue() {
        delete[] arr;
    }

    bool isEmpty() const {
        return size == 0;
    }

    int length() const {
        return size;
    }

    void enqueue(const T& value) {
        if(size == capacity) {
            throw std::runtime_error("Queue is full");
        }
        arr[tail] = value;
        tail = (tail + 1) % capacity;
        size++;
    }

    T dequeue() {
        if(isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        T value = arr[head];
        head = (head + 1) % capacity;
        size--;
        return value;
    }

    T peek() const {
        if(isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        return arr[head];
    }
};
```

Este es un ejemplo de implementación de una cola en C++ utilizando un arreglo (array). El código comienza definiendo una clase `Queue` que tiene los siguientes miembros privados:

-   `arr`: un puntero a un arreglo de elementos de tipo `T`.
  
-   `head`: un entero que representa el índice del primer elemento en la cola.

-   `tail`: un entero que representa el índice del siguiente espacio disponible en el arreglo (donde se agregará el siguiente elemento a la cola).
  
-   `capacity`: un entero que representa la capacidad máxima de la cola (el tamaño máximo del arreglo).
  
-   `size`: un entero que representa el tamaño actual de la cola.

A continuación, se definen los métodos públicos de la clase `Queue`:

-  `Queue(int cap)`: el constructor de la clase `Queue`, que toma como argumento la capacidad máxima de la cola. Dentro del constructor, se inicializan los miembros `head`, `tail`, `capacity` y `size`, y se asigna dinámicamente un arreglo de tamaño `capacity` a través del puntero `arr`.
  
-  `~Queue()`: el destructor de la clase `Queue`, que libera la memoria asignada dinámicamente para el arreglo a través del puntero `arr`.
  
-  `isEmpty() const`: un método constante que devuelve `true` si la cola está vacía y `false` en caso contrario.
  
-  `length() const`: un método constante que devuelve el tamaño actual de la cola.
  
-  `enqueue(const T& value)`: un método que agrega un nuevo elemento al final de la cola. Si la cola está llena, se lanza una excepción `std::runtime_error`. De lo contrario, se asigna el valor del nuevo elemento al índice `tail` en el arreglo y se actualiza el índice `tail` al siguiente espacio disponible en el arreglo, teniendo en cuenta que la cola es circular (si `tail` llega al final del arreglo, se "envuelve" al principio). Finalmente, se incrementa el tamaño de la cola.
  
-  `dequeue()`: un método que elimina y devuelve el primer elemento de la cola. Si la cola está vacía, se lanza una excepción `std::runtime_error`. De lo contrario, se asigna el valor del primer elemento al índice `head` en el arreglo y se actualiza el índice `head` al siguiente elemento en la cola, teniendo en cuenta que la cola es circular. Finalmente, se decrementa el tamaño de la cola y se devuelve el valor del elemento eliminado.
  
-  `peek() const`: un método constante que devuelve el valor del primer elemento de la cola sin eliminarlo. Si la cola está vacía, se lanza una excepción `std::runtime_error`.

## Lista enlazada vs Array

Tanto la implementación de cola con lista como la implementación de cola con arreglo tienen ventajas y desventajas, y la elección entre ellas dependerá de las necesidades y limitaciones específicas de cada situación.

### Implementación de cola con lista enlazada

#### Ventajas

-   La lista enlazada puede crecer o reducir de tamaño dinámicamente, lo que significa que no hay un límite en la cantidad de elementos que se pueden agregar a la cola.
-   Las operaciones de inserción y eliminación de elementos en una lista enlazada son muy eficientes, ya que solo se necesitan actualizar unos pocos punteros.

#### Desventajas

-   La lista enlazada utiliza más memoria que la implementación de la cola con arreglo, ya que cada elemento de la lista requiere un nodo adicional de puntero.
-   La implementación de la cola con lista enlazada puede ser menos eficiente en términos de acceso aleatorio, ya que para acceder a un elemento en una posición específica de la cola se debe recorrer la lista desde el principio.

### Implementación de cola con arreglo/array

#### Ventajas

-   La implementación de la cola con arreglo utiliza menos memoria que la implementación de la cola con lista, ya que solo se requiere espacio para almacenar los elementos de la cola.
-   La implementación de la cola con arreglo es muy eficiente en términos de acceso aleatorio, ya que se puede acceder directamente a cualquier elemento de la cola mediante el índice.

#### Desventajas

-   La implementación de la cola con arreglo tiene un tamaño fijo, lo que significa que hay un límite en la cantidad de elementos que se pueden agregar a la cola.
-   Las operaciones de inserción y eliminación de elementos en una cola con arreglo pueden ser ineficientes, ya que se necesitan reorganizar los elementos en el arreglo para mantener la cola en orden.

### Conclusión

En resumen, la elección entre la implementación de cola con lista y la implementación de cola con arreglo dependerá de las necesidades específicas de cada situación, como el tamaño previsto de la cola, el número de operaciones de inserción y eliminación de elementos, y la necesidad de acceso aleatorio. 

Si se espera que la cola crezca o reduzca dinámicamente de tamaño, entonces la implementación de cola con lista enlazada puede ser más adecuada. Por otro lado, si se espera que la cola tenga un tamaño fijo y se requiere un acceso aleatorio eficiente, entonces la implementación de cola con arreglo puede ser más adecuada.

# Visualización 

- https://www.cs.usfca.edu/~galles/visualization/QueueLL.html
- https://www.cs.usfca.edu/~galles/visualization/QueueArray.html

# Mas información

- https://www.geeksforgeeks.org/abstract-data-types/
- https://en.wikipedia.org/wiki/Queue_(abstract_data_type)