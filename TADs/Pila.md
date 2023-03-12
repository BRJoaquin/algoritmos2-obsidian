---
tag: TAD
---

# Intro

La pila es un [[Tipo Abstracto de Dato (TAD)]], también conocido como stack en inglés, es una estructura de datos lineal en la que los elementos se organizan siguiendo el principio de "último en entrar, primero en salir" (LIFO por sus siglas en inglés, last-in, first-out).

La pila se puede implementar utilizando un arreglo o una lista enlazada, y se caracteriza por tener dos operaciones fundamentales:

1.  **Push**: Esta operación permite agregar un nuevo elemento a la pila. El nuevo elemento se agrega en la cima de la pila, es decir, en la posición más alta. En la implementación con arreglo, esto significa agregar el elemento en la última posición disponible; en la implementación con lista enlazada, se crea un nuevo nodo que se enlaza al nodo que estaba en la cima de la pila.

2.  **Pop**: Esta operación permite retirar el elemento que se encuentra en la cima de la pila. El elemento retirado es el último que se agregó a la pila, es decir, el que está más arriba. En la implementación con arreglo, esto significa eliminar el último elemento agregado; en la implementación con lista enlazada, se elimina el nodo que está en la cima de la pila.  

Además de estas dos operaciones fundamentales, la pila también puede tener otras operaciones útiles, como:

-   **Top**: Permite consultar el elemento que se encuentra en la cima de la pila, sin retirarlo.
  
-   **IsEmpty**: Permite verificar si la pila está vacía o no.

La pila se utiliza en una gran variedad de aplicaciones, como la evaluación de expresiones aritméticas, la navegación en sistemas de historial, la implementación de undo/redo en editores de texto, entre otros.

Aunque la pila y la [[Cola]] son estructuras de datos lineales, tienen diferencias significativas en su funcionamiento. La principal diferencia es el orden en el que se agregan y se retiran los elementos. Mientras que en la pila el último elemento en entrar es el primero en salir, en la cola el primer elemento en entrar es el primero en salir.

# Defincion

```cpp
template <typename T>
class Stack {
public:

    /**
     * Description: Adds an element to the top of the stack.
     * @param value: the element to add to the stack.
     * Pre-condition: None.
     * Post-condition: A new node containing the value is added to the top of the stack.
     */
    virtual void push(T value) = 0;

    /**
     * Description: Removes and returns the element at the top of the stack.
     * @return: the element that was removed.
     * Pre-condition: The stack is not empty.
     * Post-condition: The top node is removed from the stack, and its value is returned.
     */
    virtual T pop() = 0;

    /**
     * Description: Returns the element at the top of the stack, without removing it.
     * @return: the element at the top of the stack.
     * Pre-condition: The stack is not empty.
     * Post-condition: The value at the top of the stack is returned, but the stack is not modified.
     */
    virtual T top() const = 0;

    /**
     * Description: Returns true if the stack is empty, and false otherwise.
     * @return: true if the stack is empty, false otherwise.
     * Pre-condition: None.
     * Post-condition: The state of the stack is not modified.
     */
    virtual bool isEmpty() const = 0;
};
```


# Implementacion

Existen diferentes implementaciones que se pueden utilizar para implementar una pila, algunas de ellas son:

1.  **Implementación con arreglo**: Se utiliza un arreglo de tamaño fijo para almacenar los elementos de la pila. La pila se implementa con un puntero que indica la posición del último elemento agregado. Esta implementación es sencilla y eficiente en términos de acceso a los elementos, pero puede ser ineficiente en términos de espacio si el tamaño del arreglo es grande y la pila no está llena.

2.  **Implementación con lista enlazada**: Se utiliza una [[Lista simplemente encadenada]] para almacenar los elementos de la pila. Cada nodo de la lista contiene el valor del elemento y un puntero al siguiente nodo. La pila se implementa con un puntero que apunta al nodo que está en la cima de la pila. Esta implementación es eficiente en términos de espacio, ya que no se necesita un arreglo de tamaño fijo, pero puede ser menos eficiente en términos de acceso a los elementos.

3.  **Implementación con lista doblemente enlazada**: Similar a la implementación con lista enlazada, pero cada nodo también tiene un puntero al nodo anterior. Esto permite implementar operaciones adicionales como moverse hacia atrás en la pila, pero también requiere más espacio que la implementación con lista enlazada.

## Implementacion con arrays

```cpp
template <typename T>
class ArrayStack : public Stack<T> {
public:
    ArrayStack(int capacity) : capacity_(capacity), top_(-1) {
        array_ = new T[capacity_];
    }
    ~ArrayStack() {
        delete[] array_;
    }
    void push(T value) {
        if (top_ == capacity_ - 1) {
            throw std::out_of_range("Stack overflow");
        }
        array_[++top_] = value;
    }
    T pop() {
        if (isEmpty()) {
            throw std::out_of_range("Stack underflow");
        }
        return array_[top_--];
    }
    T top() const {
        if (isEmpty()) {
            throw std::out_of_range("Stack is empty");
        }
        return array_[top_];
    }
    bool isEmpty() const {
        return top_ == -1;
    }
private:
    T* array_;
    int capacity_;
    int top_;
};
```

En esta implementación, la clase `ArrayStack` es una subclase de `Stack` que utiliza un arreglo para almacenar los elementos de la pila. El constructor toma un argumento `capacity` que especifica la capacidad máxima de la pila. El arreglo se crea dinámicamente en el constructor y se libera en el destructor.

Los métodos `push`, `pop`, `top` y `isEmpty` proporcionan la implementación de la interfaz definida por la clase base `Stack`. En el método `push`, se verifica si la pila está llena antes de agregar un nuevo elemento. En el método `pop`, se verifica si la pila está vacía antes de retirar y devolver el elemento de la cima de la pila. En el método `top`, se verifica si la pila está vacía antes de devolver el elemento de la cima de la pila sin retirarlo. En el método `isEmpty`, se verifica si la pila está vacía comparando el valor del puntero `top_` con `-1`.

## Implementacion con lista enlazada

```cpp
template <typename T>
class LinkedStack : public Stack<T> {
public:
    LinkedStack() : top_(nullptr) {}
    ~LinkedStack() {
        while (!isEmpty()) {
            pop();
        }
    }
    void push(T value) {
        Node* newNode = new Node(value, top_);
        top_ = newNode;
    }
    T pop() {
        if (isEmpty()) {
            throw std::out_of_range("Stack underflow");
        }
        Node* nodeToDelete = top_;
        top_ = top_->next;
        T value = nodeToDelete->value;
        delete nodeToDelete;
        return value;
    }
    T top() const {
        if (isEmpty()) {
            throw std::out_of_range("Stack is empty");
        }
        return top_->value;
    }
    bool isEmpty() const {
        return top_ == nullptr;
    }
private:
    struct Node {
        T value;
        Node* next;
        Node(T value, Node* next) : value(value), next(next) {}
    };
    Node* top_;
};
```

En esta implementación, la clase `LinkedStack` es una subclase de `Stack` que utiliza una lista enlazada para almacenar los elementos de la pila. La lista enlazada se implementa utilizando nodos, donde cada nodo contiene el valor de un elemento y un puntero al siguiente nodo. El puntero `top_` indica el primer nodo de la lista, que corresponde al elemento de la cima de la pila.

Los métodos `push`, `pop`, `top` y `isEmpty` proporcionan la implementación de la interfaz definida por la clase base `Stack`. En el método `push`, se crea un nuevo nodo con el valor del elemento y el puntero `next` apuntando al nodo actualmente en la cima de la pila, y se actualiza el puntero `top_` para apuntar al nuevo nodo. En el método `pop`, se verifica si la pila está vacía antes de retirar y devolver el elemento de la cima de la pila eliminando el nodo correspondiente y actualizando el puntero `top_`. En el método `top`, se verifica si la pila está vacía antes de devolver el valor del elemento de la cima de la pila sin retirarlo. En el método `isEmpty`, se verifica si la pila está vacía comparando el valor del puntero `top_` con `nullptr`.

## Ordenes

Las órdenes temporales (véase: [[Ordenes - The Big O]]) de las funciones en una implementación de pila dependen de la estructura de datos subyacente que se utilice.

Implementación con arreglo:

-   `push`: Agregar un elemento al final del arreglo es una operación de tiempo constante **O(1)**. 
-   `pop`: Eliminar el último elemento del arreglo es una operación de tiempo constante **O(1)**.
-   `top`: Devolver el último elemento del arreglo es una operación de tiempo constante **O(1)**.
-   `isEmpty`: Verificar si el arreglo está vacío es una operación de tiempo constante **O(1)**.

Implementación con lista enlazada:

-   `push`: Agregar un nuevo nodo al principio de la lista enlazada es una operación de tiempo constante **O(1)**.
-   `pop`: Eliminar el primer nodo de la lista enlazada es una operación de tiempo constante **O(1)**.
-   `top`: Devolver el valor del primer nodo de la lista enlazada es una operación de tiempo constante **O(1)**.
-   `isEmpty`: Verificar si la lista enlazada está vacía es una operación de tiempo constante **O(1)**.

Es importante tener en cuenta que estas órdenes temporales se refieren al peor de los casos, es decir, al tiempo máximo que puede tardar la función en ejecutarse. En la implementación con arreglo, la función `push` puede ser más lenta en casos raros cuando es necesario redimensionar el arreglo (en caso que se quiera implementar una estructura infinita), pero en promedio sigue siendo O(1). En la implementación con lista enlazada, se puede tener un consumo adicional de memoria por los nodos que se crean.

En general, ambas implementaciones son eficientes en términos de tiempo de ejecución y pueden ser adecuadas para diferentes situaciones dependiendo de los requisitos específicos de la aplicación.