# Intro

Una lista es un tipo abstracto de datos ([[Tipo Abstracto de Dato (TAD)]]) que se utiliza para modelar una estructura linealmente ordenada de elementos, donde se define una interfaz abstracta que especifica las operaciones permitidas y sus restricciones. Las operaciones más comunes incluyen la inserción, eliminación y acceso a elementos individuales en una lista.

# Definicion de operaciones

```cpp
#ifndef LIST_H
#define LIST_H

template <typename T>
class List {
public:
    // Constructs an empty list.
    List();

    // Copy constructor.
    // Pre-condition: 'other' is a valid list object.
    // Post-condition: This list is a deep copy of 'other'.
    List(const List<T>& other);

    // Destructor.
    // Post-condition: All dynamically allocated memory for this list has been freed.
    ~List();

    // Adds an item to the back of the list.
    // Post-condition: The size of the list has increased by 1.
    void push_back(const T& item);

    // Adds an item to the front of the list.
    // Post-condition: The size of the list has increased by 1.
    void push_front(const T& item);

    // Removes the item at the back of the list.
    // Pre-condition: The list is not empty.
    // Post-condition: The size of the list has decreased by 1.
    void pop_back();

    // Removes the item at the front of the list.
    // Pre-condition: The list is not empty.
    // Post-condition: The size of the list has decreased by 1.
    void pop_front();

	// Get a element at certain position
	// Pre-condition: A valid position (zero based)
	T& get(int i);

    // Removes all items from the list.
    // Post-condition: The size of the list is 0 and all dynamically allocated memory has been freed.
    void clear();

    // Returns a reference to the item at the front of the list.
    // Pre-condition: The list is not empty.
    T& front() const;

    // Returns a reference to the item at the back of the list.
    // Pre-condition: The list is not empty.
    T& back() const;

    // Returns the number of items in the list.
    int size() const;

    // Returns true if the list is empty, false otherwise.
    bool empty() const;

	// Returns true if the size of the list has reached the maximum 
	// capacity, false otherwise. 
	bool full() const;
};

#endif // LIST_H
```

# Implementaciones

Existen diferentes implementaciones para una lista, algunas de las más comunes son las siguientes:

1. Arreglos o arrays: Es una estructura de datos que puede almacenar un conjunto de elementos del mismo tipo en una secuencia continua de memoria. Las listas se pueden implementar utilizando arreglos, donde cada elemento de la lista se almacena en una posición diferente del arreglo. Tiene como ventaja poder acceder a cualquier posición de la lista en O(1)pc pero esta limitada con su tamaño finito.

2. [[Lista simplemente encadenada]]: Es una estructura de datos que consta de nodos, donde cada nodo almacena un elemento y **una referencia al siguiente nodo en la lista**. Las listas simplemente encadenadas son una fácil implementacion y una de las mas populares para implementar el TAD Lista. 

3. [[Lista doblemente encadenada]]: Son similares a las listas simplemente encadenadas, pero cada nodo tiene una referencia tanto al nodo siguiente como al anterior.


# Mas información
