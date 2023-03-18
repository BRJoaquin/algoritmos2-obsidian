---
tag: TAD
---
# Intro
Una tabla o ==diccionario== es un Tipo Abstracto de Datos (TAD) que define una colección desordenada de datos en forma de pares ==clave==-==valor==. Cada clave, que **debe ser única**, tiene un valor asociado. Por lo general, las claves en un diccionario deben ser de tipos simples (como enteros o cadenas de caracteres) mientras que los valores pueden ser de cualquier tipo.

![[Pasted image 20230318115003.png]]

Las operaciones estándar de un diccionario incluyen:

1.  Recuperar un valor asociado a una clave específica: permite obtener el valor correspondiente a una clave dada.
2.  Insertar un nuevo par clave-valor en la colección: agrega un nuevo elemento al diccionario, conformado por la clave y su valor asociado. De ya existir la clave, actualiza el valor.
3.  Eliminar un par clave-valor de la colección: remueve el elemento identificado por la clave del diccionario.

El uso de una clave permite el acceso directo a los elementos almacenados en la colección. Esto ofrece un acceso mucho más rápido a los datos desordenados en comparación con la búsqueda en el conjunto de datos mediante una búsqueda lineal y también será más eficiente que una búsqueda binaria. La recuperación de valores mediante claves es una técnica ampliamente utilizada en la informática, especialmente en estructuras de datos como [[Tabla de hash]].

# Ejemplo de especificación

```cpp
#include <iostream>
#include <unordered_map>
#include <string>
#include <stdexcept>

class Dictionary {
public:
    // Precondición: ninguna.
    // Postcondición: el par clave-valor se agregará al diccionario. De existir la clave, actualiza el valor.
    virtual void insert(const std::string& key, int value) = 0;

    // Precondición: la clave debe estar en el diccionario.
    // Postcondición: devuelve el valor asociado con la clave.
    virtual int retrieve(const std::string& key) const = 0;

    // Precondición: ninguna.
    // Postcondición: elimina el par clave-valor del diccionario (de existir la clave).
    virtual void remove(const std::string& key) = 0;

	// Precondición: ninguna.
	// Postcondición: devuelve si la clave existe en el diccionario.
	virtual bool exists(const std::string& key) const = 0;
};
```

# Implementación

Muchas de las estructuras simples como [[Lista simplemente encadenada]] son suficientes para implementar la especificación de la Tabla, pero sin duda una de las mas populares debido a su eficiencia es la [[Tabla de hash]]