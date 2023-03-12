---
tag: estructura_de_datos
---
# Intro

Un árbol binario de búsqueda (BST, por sus siglas en inglés) es una [[Estructura de datos]] jerárquica en la que cada nodo tiene como máximo dos hijos, llamados hijo izquierdo y hijo derecho. Además, cada nodo tiene un valor asociado, que se utiliza para mantener un ordenamiento específico en el árbol.

La propiedad fundamental de un BST es que **el valor de cada nodo en el subárbol izquierdo es menor que el valor del nodo en sí, y el valor de cada nodo en el subárbol derecho es mayor que el valor del nodo en sí**. Esto significa que, si se busca un valor en el árbol, se puede realizar una búsqueda binaria eficiente para encontrarlo.

La raíz del árbol es el nodo principal desde el cual se ramifican todos los demás nodos. El hijo izquierdo de un nodo tiene un valor menor que el valor del nodo padre, mientras que el hijo derecho tiene un valor mayor. Si un nodo no tiene un hijo izquierdo o derecho, se considera que ese hijo es nulo.

La operación de inserción de un nuevo nodo en un BST implica buscar el lugar apropiado para el nodo y luego agregarlo como un nuevo nodo hoja en ese lugar. La eliminación de un nodo es un poco más complicada, ya que se debe garantizar que la propiedad de ordenamiento se mantenga intacta después de la eliminación.

El recorrido de un BST implica visitar cada nodo en un orden específico. Hay tres tipos principales de recorridos: **inorden**, **preorden** y **postorden**. El recorrido inorden visita los nodos en orden ascendente de valor, el recorrido preorden visita primero la raíz, luego el subárbol izquierdo y finalmente el subárbol derecho, y el recorrido postorden visita primero el subárbol izquierdo, luego el subárbol derecho y finalmente la raíz.

En resumen, un árbol binario de búsqueda es una estructura de datos eficiente y útil que mantiene un ordenamiento específico de sus nodos. Permite una búsqueda binaria eficiente y admite operaciones de inserción y eliminación. Además, se puede recorrer de diferentes maneras para realizar diferentes tareas.

# Implementacion 

```cpp
#include <iostream>

template <typename T>
class BinarySearchTree {
public:
    // Estructura de datos del nodo del ABB
    struct Node {
        T data;
        Node* left;
        Node* right;
        Node(T value) : data(value), left(nullptr), right(nullptr) {}
    };

    // Constructor y destructor
    BinarySearchTree() : root(nullptr) {}
    ~BinarySearchTree() { clear(); }

    // Métodos principales
    void insert(T value) {
        root = insertHelper(root, value);
    }

    bool search(T value) {
        return searchHelper(root, value);
    }

    void remove(T value) {
        root = removeHelper(root, value);
    }

    void clear() {
        clearHelper(root);
        root = nullptr;
    }

    void printInOrder() {
        printInOrderHelper(root);
        std::cout << std::endl;
    }

    void printPreOrder() {
        printPreOrderHelper(root);
        std::cout << std::endl;
    }

    void printPostOrder() {
        printPostOrderHelper(root);
        std::cout << std::endl;
    }

private:
    Node* root;

    // Ayuda para insertar un nuevo valor en el ABB
    Node* insertHelper(Node* node, T value) {
        if (node == nullptr) {
            return new Node(value);
        }
        if (value < node->data) {
            node->left = insertHelper(node->left, value);
        }
        else if (value > node->data) {
            node->right = insertHelper(node->right, value);
        }
        return node;
    }

    // Ayuda para buscar un valor dado en el ABB
    bool searchHelper(Node* node, T value) {
        if (node == nullptr) {
            return false;
        }
        if (value == node->data) {
            return true;
        }
        else if (value < node->data) {
            return searchHelper(node->left, value);
        }
        else {
            return searchHelper(node->right, value);
        }
    }

    // Ayuda para eliminar un valor dado del ABB
    Node* removeHelper(Node* node, T value) {
        if (node == nullptr) {
            return nullptr;
        }
        if (value < node->data) {
            node->left = removeHelper(node->left, value);
        }
        else if (value > node->data) {
            node->right = removeHelper(node->right, value);
        }
        else {
            if (node->left == nullptr) {
                Node* temp = node->right;
                delete node;
                return temp;
            }
            else if (node->right == nullptr) {
                Node* temp = node->left;
                delete node;
                return temp;
            }
            Node* temp = findMinNode(node->right);
            node->data = temp->data;
            node->right = removeHelper(node->right, temp->data);
        }
        return node;
    }

    // Encuentra el nodo con el valor mínimo en el subárbol dado
    Node* findMinNode(Node* node) {
        while (node->left != nullptr) {
            node = node->left;
        }
        return node;
    }

    // Ayuda para eliminar todos los nodos del ABB
    void clearHelper(Node* node) {
		if (node != nullptr) {
			clearHelper(node->left);
			clearHelper(node->right);
			delete node;
		}
	}
		
	// Ayuda para imprimir los valores del ABB en orden
	void printInOrderHelper(Node* node) {
		if (node != nullptr) {
			printInOrderHelper(node->left);
			std::cout << node->data << " ";
			printInOrderHelper(node->right);
		}
	}
	
	// Ayuda para imprimir los valores del ABB en preorden
	void printPreOrderHelper(Node* node) {
		if (node != nullptr) {
			std::cout << node->data << " ";
			printPreOrderHelper(node->left);
			printPreOrderHelper(node->right);
		}
	}
	
	// Ayuda para imprimir los valores del ABB en postorden
	void printPostOrderHelper(Node* node) {
		if (node != nullptr) {
			printPostOrderHelper(node->left);
			printPostOrderHelper(node->right);
			std::cout << node->data << " ";
		}
	}
}

```

-   `insert(T value)`: este método inserta un nuevo valor `value` en el árbol. Primero, se llama a la función `insertHelper` para insertar el valor en el árbol, pasando como argumento el nodo raíz del árbol y el valor a insertar. Si la raíz es nula, se crea un nuevo nodo con el valor `value`. Si el valor es menor que el valor del nodo actual, se busca en el subárbol izquierdo, y si es mayor, se busca en el subárbol derecho. El método devuelve el nodo raíz actualizado con el nuevo valor.

-   `search(T value)`: este método busca si un valor `value` dado se encuentra en el árbol. Se llama a la función `searchHelper` para realizar la búsqueda, pasando como argumento el nodo raíz del árbol y el valor a buscar. Si el nodo es nulo, el valor no se encuentra en el árbol. Si el valor es igual al valor del nodo actual, se ha encontrado el valor y se devuelve `true`. Si el valor es menor que el valor del nodo actual, se busca en el subárbol izquierdo, y si es mayor, se busca en el subárbol derecho. El método devuelve `true` si el valor se encuentra en el árbol y `false` en caso contrario.

-   `remove(T value)`: este método elimina un valor `value` dado del árbol. Primero, se llama a la función `removeHelper` para eliminar el valor del árbol, pasando como argumento el nodo raíz del árbol y el valor a eliminar. Si el nodo es nulo, no se hace nada y se devuelve el nodo actual. Si el valor es menor que el valor del nodo actual, se busca en el subárbol izquierdo, y si es mayor, se busca en el subárbol derecho. Si se encuentra el valor, se procede a eliminarlo. Si el nodo a eliminar no tiene hijos, simplemente se elimina el nodo. Si el nodo a eliminar tiene un solo hijo, se elimina el nodo y se devuelve su hijo. Si el nodo a eliminar tiene dos hijos, se encuentra el nodo con el valor mínimo en el subárbol derecho del nodo actual, se intercambia el valor de ese nodo con el valor del nodo a eliminar y se elimina el nodo mínimo. El método devuelve el nodo raíz actualizado sin el valor eliminado.

-   `clear()`: este método elimina todos los nodos del árbol. Se llama a la función `clearHelper` para eliminar todos los nodos del árbol, pasando como argumento el nodo raíz del árbol. La función realiza una eliminación post-orden recursiva para eliminar cada nodo del árbol.

# Recorridas

En un árbol binario de búsqueda (ABB), los recorridos son las técnicas utilizadas para visitar todos los nodos del árbol. Hay tres tipos principales de recorridos en los ABB:

1.  **Recorrido en orden** (in-order traversal): En este recorrido, primero se visita el subárbol izquierdo, luego se visita el nodo actual y finalmente se visita el subárbol derecho. El recorrido en orden produce una lista ordenada de los elementos del árbol en orden ascendente.

```cpp
void inOrderTraversal(Node* root) {
    if (root == nullptr) {
        return;
    }
    inOrderTraversal(root->left); // Visita el subárbol izquierdo
    cout << root->data << " "; // Visita el nodo actual
    inOrderTraversal(root->right); // Visita el subárbol derecho
}
```

2.  **Recorrido en preorden** (pre-order traversal): En este recorrido, primero se visita el nodo actual, luego se visita el subárbol izquierdo y finalmente se visita el subárbol derecho. El recorrido en preorden produce una lista de elementos en el orden en que se encuentran en el árbol.

```cpp
void preOrderTraversal(Node* root) {
    if (root == nullptr) {
        return;
    }
    cout << root->data << " "; // Visita el nodo actual
    preOrderTraversal(root->left); // Visita el subárbol izquierdo
    preOrderTraversal(root->right); // Visita el subárbol derecho
}
```

3.  **Recorrido en postorden** (post-order traversal): En este recorrido, primero se visita el subárbol izquierdo, luego se visita el subárbol derecho y finalmente se visita el nodo actual. El recorrido en postorden produce una lista de elementos en el orden inverso al que se encuentran en el árbol.
   
```cpp
void postOrderTraversal(Node* root) {
    if (root == nullptr) {
        return;
    }
    postOrderTraversal(root->left); // Visita el subárbol izquierdo
    postOrderTraversal(root->right); // Visita el subárbol derecho
    cout << root->data << " "; // Visita el nodo actual
}
```

Cada tipo de recorrido tiene diferentes aplicaciones. Por ejemplo, el recorrido en orden se utiliza comúnmente para imprimir los elementos del ABB en orden ascendente, mientras que el recorrido en postorden se utiliza para liberar la memoria asignada a los nodos del árbol. Además, los recorridos se pueden combinar con otras técnicas de procesamiento de datos para realizar operaciones más complejas en los ABB.

# Degradación del ABB (desbalanceo)

Si los elementos se insertan en el árbol de manera ordenada, por ejemplo, en orden ascendente o descendente, se puede llegar a una situación en la que el árbol se convierte en una [[Lista simplemente encadenada]]. En este caso, el tiempo (vease: [[Ordenes - The Big O]]) de búsqueda, inserción y eliminación de elementos en el árbol se convierte en O(N), donde N es el número de elementos en el árbol.

Para entender por qué esto ocurre, es importante recordar cómo se insertan elementos en un BST. Cuando se inserta un elemento en un BST, se compara con la raíz del árbol. Si es menor, se inserta en el subárbol izquierdo, y si es mayor, se inserta en el subárbol derecho. Este proceso se repite hasta encontrar una hoja vacía en la que se inserta el elemento.

Si los elementos se insertan en orden ascendente, cada nuevo elemento será mayor que el anterior y se insertará en el subárbol derecho del último nodo insertado. Como resultado, el árbol se convierte en una lista enlazada que se extiende hacia la derecha, y cada nodo tiene solo un hijo (el de la derecha). El mismo principio se aplica si los elementos se insertan en orden descendente, pero la lista enlazada se extiende hacia la izquierda.

En este caso, el tiempo de búsqueda, inserción y eliminación de elementos en el árbol se convierte en O(N), ya que se tiene que recorrer todo el árbol para realizar estas operaciones. Esto es mucho menos eficiente que O(logN) y significa que el uso de BST en este caso es inapropiado.

Para evitar que esto ocurra, se pueden utilizar diferentes técnicas de equilibrado de árboles, como el árbol [[AVL]], que garantizan que el árbol se mantenga balanceado y evite convertirse en una lista enlazada.

## Probabilidad de desgradacion

En el mundo real, la probabilidad de que un árbol binario de búsqueda (ABB) esté **tan desequilibrado** que afecte significativamente su rendimiento depende de varios factores, como el tipo de aplicación, la cantidad de datos y la distribución de los datos.

**En general, la probabilidad de que un ABB esté muy desequilibrado disminuye a medida que aumenta el número de nodos en el árbol** y la distribución de los datos se vuelve más uniforme. En otras palabras, cuanto más grande es el árbol y más uniformemente distribuidos están los datos, menos probable es que el árbol esté desequilibrado.

Sin embargo, en algunos casos, puede haber una serie de inserciones o eliminaciones que resulten en un árbol ABB muy desequilibrado, lo que puede afectar significativamente su rendimiento.

# Ordenes temporales

-   `insert(T value)`: el caso promedio ocurre cuando el árbol está balanceado (o cerca de estarlo). En este caso, se necesitan **O(log n)** comparaciones para encontrar la ubicación correcta del nuevo valor en el árbol. En el peor caso, el árbol no está balanceado, y se necesitan **O(n)** comparaciones para encontrar la ubicación correcta del nuevo valor. Por lo tanto, el orden temporal en el caso promedio y peor caso es O(n).

-   `search(T value)`: el caso promedio y peor caso son los mismos en este método. El peor caso ocurre cuando el árbol está completamente desbalanceado, lo que significa que se necesita recorrer todo el árbol para encontrar el valor. En este caso, se necesitan **O(n)** comparaciones para encontrar el valor. En el caso promedio, se espera que el árbol esté balanceado, y por lo tanto, se necesitan **O(log n)** comparaciones para encontrar el valor.

-   `remove(T value)`:  el peor caso ocurre cuando el árbol está completamente desbalanceado, lo que significa que se necesita recorrer todo el árbol para encontrar el nodo a eliminar. En este caso, se necesitan **O(n)** comparaciones para encontrar el nodo a eliminar. En el caso promedio, se espera que el árbol esté balanceado, y por lo tanto, se necesitan **O(log n)** comparaciones para encontrar el nodo a eliminar.

-   `clear()`: este método elimina todos los nodos del árbol en un recorrido post-orden, lo que significa que cada nodo se visita exactamente una vez. Por lo tanto, el orden temporal en el caso promedio y peor caso es **O(n)**, donde n es el número de nodos en el árbol.

-   `printInOrder()`, `printPreOrder()` y `printPostOrder()`: cada uno de estos métodos recorre todo el árbol e imprime cada valor del árbol una vez. Por lo tanto, el orden temporal en el caso promedio y peor caso es **O(n)**, donde n es el número de nodos en el árbol.

# Usos

1.  **Búsqueda de datos**: Los ABB son muy eficientes en la búsqueda de datos. Como cada nodo tiene dos hijos (izquierdo y derecho), se puede ir descartando la mitad de los elementos en cada comparación. Por esta razón, se utilizan ABB en aplicaciones donde es necesario realizar búsquedas de manera rápida y eficiente, como en bases de datos, buscadores en internet, entre otros.

2.  **Implementación de diccionarios y mapas**: Los ABB se pueden utilizar para implementar diccionarios y mapas. En este caso, cada elemento del árbol representa una clave-valor, donde la clave se utiliza para buscar el valor asociado. Los ABB permiten una inserción, búsqueda y eliminación eficiente de los elementos en el diccionario o mapa.

3.  **Ordenación de datos**: Los ABB se pueden utilizar para ordenar datos en tiempo O(nlogn), donde n es el número de elementos a ordenar. Para ello, se insertan los elementos en el árbol y luego se recorre el árbol en orden inorden. De esta forma, se obtienen los elementos ordenados.

4.  **Análisis de datos**: Los ABB se utilizan en la implementación de algoritmos de análisis de datos como el árbol de decisión y la clasificación de datos. En este caso, el árbol representa el conjunto de reglas de decisión que se utilizan para clasificar los datos.

5.  **Compresión de datos**: Los ABB se pueden utilizar en la implementación de algoritmos de compresión de datos, como el algoritmo de [Huffman](https://es.wikipedia.org/wiki/Algoritmo_de_Huffman). En este caso, el árbol se utiliza para asignar códigos de compresión a los elementos, donde los elementos más frecuentes se asignan códigos más cortos.

En general, los ABB son una estructura de datos muy versátil y se utilizan en una gran cantidad de aplicaciones. Su eficiencia en la búsqueda y ordenación de datos, así como su facilidad de implementación, los hacen muy populares en el desarrollo de software.


# Visualización

https://www.cs.usfca.edu/~galles/visualization/BST.html 

# Mas info

- https://www.geeksforgeeks.org/binary-search-tree-data-structure/