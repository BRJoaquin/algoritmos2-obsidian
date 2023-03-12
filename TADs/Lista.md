---
tag: TAD
---
# Intro

Una lista es un [[Tipo Abstracto de Dato (TAD)]] que se utiliza para modelar una estructura linealmente ordenada de elementos, donde se define una interfaz abstracta que especifica las operaciones permitidas y sus restricciones. Las operaciones más comunes incluyen la inserción, eliminación y acceso a elementos individuales en una lista.

# Definicion de operaciones

```cpp
#ifndef LIST_H
#define LIST_H

template <typename T>
class List {
public:

    // Adds an item to the back of the list.
    // Post-condition: The size of the list has increased by 1.
    virtual void push_back(const T& item) = 0;

    // Adds an item to the front of the list.
    // Post-condition: The size of the list has increased by 1.
    virtual void push_front(const T& item) = 0;

    // Removes the item at the back of the list.
    // Pre-condition: The list is not empty.
    // Post-condition: The size of the list has decreased by 1.
    virtual void pop_back() = 0;

    // Removes the item at the front of the list.
    // Pre-condition: The list is not empty.
    // Post-condition: The size of the list has decreased by 1.
    virtual void pop_front() = 0;

	// Get a element at certain position
	// Pre-condition: A valid position (zero based)
	virtual T& get(int i);

    // Removes all items from the list.
    // Post-condition: The size of the list is 0 and all dynamically allocated memory has been freed.
    virtual void clear() = 0;

    // Returns a reference to the item at the front of the list.
    // Pre-condition: The list is not empty.
    virtual T& front() const = 0;

    // Returns a reference to the item at the back of the list.
    // Pre-condition: The list is not empty.
    virtual T& back() const = 0;

    // Returns the number of items in the list.
    virtual int size() const = 0;

    // Returns true if the list is empty, false otherwise.
    virtual bool empty() const = 0;

	// Returns true if the size of the list has reached the maximum 
	// capacity, false otherwise. 
	virtual bool full() const = 0;
};

#endif // LIST_H
```

# Implementaciones

Existen diferentes implementaciones para una lista, algunas de las más comunes son las siguientes:

1. Arreglos o arrays: Es una estructura de datos que puede almacenar un conjunto de elementos del mismo tipo en una secuencia continua de memoria. Las listas se pueden implementar utilizando arreglos, donde cada elemento de la lista se almacena en una posición diferente del arreglo. Tiene como ventaja poder acceder a cualquier posición de la lista en O(1)pc pero esta limitada con su tamaño finito.

2. [[Lista simplemente encadenada]]: Es una estructura de datos que consta de nodos, donde cada nodo almacena un elemento y **una referencia al siguiente nodo en la lista**. Las listas simplemente encadenadas son una fácil implementacion y una de las mas populares para implementar el TAD Lista. 

3. [[Lista doblemente encadenada]]: Son similares a las listas simplemente encadenadas, pero cada nodo tiene una referencia tanto al nodo siguiente como al anterior.


# Mas información

- https://en.wikipedia.org/wiki/List_(abstract_data_type)
- https://opendsa-server.cs.vt.edu/ODSA/Books/CS3/html/ListADT.html
