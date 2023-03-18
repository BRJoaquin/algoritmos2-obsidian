---
tag: estructura_de_datos
---
# Intro

Los árboles AVL son una [[Estructura de datos]] de árbol binario que se utilizan para almacenar y buscar datos de manera eficiente. Fueron inventados por los matemáticos Adelson-Velsky y Landis en 1962.

**La característica principal de los árboles AVL es que mantienen una altura balanceada.** Esto significa que la altura de los subárboles izquierdo y derecho de cada nodo difiere en un máximo de una unidad. Para lograr esto, los árboles AVL se reorganizan automáticamente después de cada inserción o eliminación de un nodo, para mantener el equilibrio.

El equilibrio se mantiene mediante la **rotación** de los subárboles del árbol AVL. Una rotación es una operación que cambia la estructura del árbol al mover un subárbol hacia arriba o hacia abajo en el árbol. Los árboles AVL pueden ser rotados hacia la izquierda o hacia la derecha dependiendo de la situación.

La ventaja de mantener un equilibrio en los árboles AVL es que la altura del árbol **se mantiene en logarítmico en función del número de nodos**, lo que permite que las operaciones de búsqueda, inserción y eliminación se realicen en tiempo logarítmico. Esto los hace ideales para aplicaciones en las que se necesite una rápida búsqueda y actualización de datos, como bases de datos y sistemas de indexación.

En resumen, los árboles AVL son una estructura de datos de árbol binario que mantiene una altura balanceada a través de rotaciones automáticas después de cada inserción o eliminación de un nodo. El equilibrio permite que las operaciones de búsqueda, inserción y eliminación se realicen en tiempo logarítmico, lo que los hace ideales para aplicaciones en las que se necesite una rápida búsqueda y actualización de datos.

# Autobalance

El autobalance es una característica clave de los árboles AVL, que garantiza que el árbol esté siempre equilibrado. La detección de desequilibrios y la rotación de los subárboles para mantener el equilibrio se realiza automáticamente en tiempo constante después de cada operación de inserción o eliminación.

Existen cuatro casos posibles de desequilibrio en un árbol AVL, que se determinan por el factor de balance de cada nodo en el árbol:

1.  **Caso izquierda-izquierda** (LL): este caso ocurre cuando el factor de balance del nodo actual es mayor que 1 y el factor de balance de su hijo izquierdo es también mayor que 1. Esto significa que el subárbol izquierdo del hijo izquierdo es más alto que el subárbol derecho del hijo izquierdo. En este caso, se realiza una rotación hacia la derecha del nodo actual.

2.  **Caso izquierda-derecha** (LR): este caso ocurre cuando el factor de balance del nodo actual es mayor que 1 y el factor de balance de su hijo izquierdo es menor que -1. Esto significa que el subárbol derecho del hijo izquierdo es más alto que el subárbol izquierdo del hijo izquierdo. En este caso, se realiza primero una rotación hacia la izquierda del hijo izquierdo y luego una rotación hacia la derecha del nodo actual.

3.  **Caso derecha-derecha** (RR): este caso ocurre cuando el factor de balance del nodo actual es menor que -1 y el factor de balance de su hijo derecho es también menor que -1. Esto significa que el subárbol derecho del hijo derecho es más alto que el subárbol izquierdo del hijo derecho. En este caso, se realiza una rotación hacia la izquierda del nodo actual.

4.  **Caso derecha-izquierda** (RL): este caso ocurre cuando el factor de balance del nodo actual es menor que -1 y el factor de balance de su hijo derecho es mayor que 1. Esto significa que el subárbol izquierdo del hijo derecho es más alto que el subárbol derecho del hijo derecho. En este caso, se realiza primero una rotación hacia la derecha del hijo derecho y luego una rotación hacia la izquierda del nodo actual.

> Nota: los factores de balance de ejemplo son siempre calculando el balance como la resta de la altura del sub-árbol izquierdo menos la altura del sub-árbol derecho.

# Implementación

## Inserción

```cpp
#include <iostream>
#include <algorithm> // Para la función max()
using namespace std;

// Clase que representa un nodo en el árbol AVL
template <class T>
class AVLNode {
public:
    T key;
    AVLNode<T>* left;
    AVLNode<T>* right;
    int height;

    // Constructor
    AVLNode(T k) {
        key = k;
        left = NULL;
        right = NULL;
        height = 1;
    }
};

// Clase que representa el árbol AVL
template <class T>
class AVLTree {
public:
    AVLNode<T>* root;

    // Constructor
    AVLTree() {
        root = NULL;
    }

    // Función para obtener la altura de un nodo
    int height(AVLNode<T>* node) {
        if (node == NULL) {
            return 0;
        }
        return node->height;
    }

    // Función para obtener el factor de balance de un nodo
    int balanceFactor(AVLNode<T>* node) {
        if (node == NULL) {
            return 0;
        }
        return height(node->left) - height(node->right);
    }

    // Función para rotar a la derecha el subárbol con raíz en el nodo 'y'
    AVLNode<T>* rightRotate(AVLNode<T>* y) {
        AVLNode<T>* x = y->left;
        AVLNode<T>* T2 = x->right;

        // Realizar la rotación
        x->right = y;
        y->left = T2;

        // Actualizar alturas
        y->height = max(height(y->left), height(y->right)) + 1;
        x->height = max(height(x->left), height(x->right)) + 1;

        return x;
    }

    // Función para rotar a la izquierda el subárbol con raíz en el nodo 'x'
    AVLNode<T>* leftRotate(AVLNode<T>* x) {
        AVLNode<T>* y = x->right;
        AVLNode<T>* T2 = y->left;

        // Realizar la rotación
        y->left = x;
        x->right = T2;

        // Actualizar alturas
        x->height = max(height(x->left), height(x->right)) + 1;
        y->height = max(height(y->left), height(y->right)) + 1;

        return y;
    }

    // Función para insertar un nodo en el árbol AVL
    AVLNode<T>* insertNode(AVLNode<T>* node, T key) {
        // Realizar la inserción de manera normal
        if (node == NULL) {
            return new AVLNode<T>(key);
        }
        if (key < node->key) {
            node->left = insertNode(node->left, key);
        } else {
            node->right = insertNode(node->right, key);
        }

        // Actualizar la altura del nodo actual
        node->height = 1 + max(height(node->left), height(node->right));

        // Obtener el factor de balance del nodo actual
        int balance = balanceFactor(node);

        // Caso 1: el nodo está desbalanceado y la clave a insertar es menor que la clave del nodo izquierdo de su hijo izquierdo
		if (balance > 1 && key < node->left->key) {
			return rightRotate(node); 
		}

		    // Caso 2: el nodo está desbalanceado y la clave a insertar es mayor que la clave de su hijo derecho
	    if (balance < -1 && key > node->right->key) {
	        return leftRotate(node);
	    }
	
	    // Caso 3: el nodo está desbalanceado y la clave a insertar es mayor que la clave de su hijo izquierdo
	    if (balance > 1 && key > node->left->key) {
	        node->left = leftRotate(node->left);
	        return rightRotate(node);
	    }
	
	    // Caso 4: el nodo está desbalanceado y la clave a insertar es menor que la clave de su hijo derecho
	    if (balance < -1 && key < node->right->key) {
	        node->right = rightRotate(node->right);
	        return leftRotate(node);
	    }
	
	    // Devolver el nodo actualizado
	    return node;
	}
	
	// Función para insertar un nodo en el árbol AVL
	void insert(T key) {
	    root = insertNode(root, key);
	}
	
	// Función para imprimir el árbol AVL en orden
	void inorderTraversal(AVLNode<T>* node) {
	    if (node != NULL) {
	        inorderTraversal(node->left);
	        cout << node->key << " ";
	        inorderTraversal(node->right);
	    }
	}
	
	// Función para imprimir el árbol AVL
	void printTree() {
	    inorderTraversal(root);
	    cout << endl;
	}
};

int main() { 
	AVLTree<int> tree;
	// Insertar nodos 
	tree.insert(10);
	tree.insert(20);
	tree.insert(30);
	tree.insert(40);
	tree.insert(50);
	tree.insert(25); 
	// Imprimir el árbol AVL 
	tree.printTree(); 
	return 0;
}
```

## Eliminación

```cpp
// Función para encontrar el nodo con el valor mínimo en el subárbol con raíz en el nodo actual
template <class T>
AVLNode<T>* minValueNode(AVLNode<T>* node) {
    AVLNode<T>* current = node;

    // Iterar hacia la izquierda hasta encontrar el nodo con el valor mínimo
    while (current->left != NULL) {
        current = current->left;
    }

    return current;
}

// Función para eliminar un nodo del árbol AVL
template <class T>
AVLNode<T>* deleteNode(AVLNode<T>* root, T key) {
    // Paso 1: realizar la eliminación normal de un nodo de un árbol binario de búsqueda
    if (root == NULL) {
        return root;
    }
    if (key < root->key) {
        root->left = deleteNode(root->left, key);
    } else if (key > root->key) {
        root->right = deleteNode(root->right, key);
    } else {
        // El nodo a eliminar es encontrado
        // Paso 2: realizar la eliminación del nodo según el caso
        if (root->left == NULL || root->right == NULL) {
            // Caso 1: el nodo a eliminar tiene uno o ningún hijo
            AVLNode<T>* temp = root->left ? root->left : root->right;

            // Si no tiene hijos, simplemente se elimina el nodo
            if (temp == NULL) {
                temp = root;
                root = NULL;
            } else {
                // Si tiene un hijo, se copia el contenido del hijo al nodo a eliminar y se elimina el hijo
                *root = *temp;
            }

            // Liberar la memoria del nodo eliminado
            delete temp;
        } else {
            // Caso 2: el nodo a eliminar tiene dos hijos
            // Encontrar el nodo con el valor mínimo en el subárbol derecho
            AVLNode<T>* temp = minValueNode(root->right);

            // Copiar el contenido del nodo mínimo al nodo actual
            root->key = temp->key;

            // Eliminar el nodo mínimo
            root->right = deleteNode(root->right, temp->key);
        }
    }

    // Si el árbol tiene solo un nodo o ninguno, se retorna el mismo árbol
    if (root == NULL) {
        return root;
    }

    // Paso 3: actualizar la altura del nodo actual
    root->height = 1 + max(height(root->left), height(root->right));

    // Paso 4: obtener el factor de balance del nodo actual
    int balance = balanceFactor(root);

    // Caso 1: el nodo está desbalanceado y la clave eliminada es menor que la clave del nodo izquierdo de su hijo izquierdo
    if (balance > 1 && balanceFactor(root->left) >= 0) {
        return rightRotate(root);
    }

    // Caso 2: el nodo está desbalanceado y la clave eliminada es mayor que la clave del nodo derecho de su hijo derecho
    if (balance < -1 && balanceFactor(root->right) <= 0) {
        return leftRotate(root);
    }

    // Caso 3: el nodo está desbalanceado y la clave eliminada es mayor que la clave del nodo izquierdo de su hijo izquierdo
   if (balance > 1 && balanceFactor(root->left) < 0) { 
	   root->left = leftRotate(root->left); 
	   return rightRotate(root); 
	}

	// Caso 4: el nodo está desbalanceado y la clave eliminada es menor que la clave del nodo derecho de su hijo derecho
	if (balance < -1 && balanceFactor(root->right) > 0) {
	    root->right = rightRotate(root->right);
	    return leftRotate(root);
	}
	
	// Devolver el nodo actualizado
	return root;
}

```


Esta función utiliza la función `minValueNode` para encontrar el nodo con el valor mínimo en el subárbol derecho del nodo a eliminar. Luego, se realiza la eliminación normal de un nodo de un árbol binario de búsqueda, según el caso (cuando el nodo a eliminar tiene uno o ningún hijo, o dos hijos). 

Después de la eliminación, se actualiza la altura del nodo actual y se obtiene el factor de balance. Si el nodo está desbalanceado, se realizan las rotaciones correspondientes para mantener el equilibrio, en los mismos cuatro casos descritos anteriormente.

# Cantidad de rotaciones

En general, la cantidad de rotaciones necesarias para mantener el equilibrio en un árbol AVL durante la inserción y la eliminación depende de la estructura del árbol y de la ubicación del nodo que se está insertando o eliminando. Sin embargo, podemos hacer algunas observaciones generales:

En la inserción, la cantidad de rotaciones necesarias es generalmente menor que en la eliminación. Esto se debe a que la inserción siempre agrega un nuevo nodo a una hoja en el árbol, mientras que la eliminación puede afectar a múltiples nodos en diferentes niveles del árbol.

En la mayoría de los casos, la inserción en un árbol AVL solo requiere una rotación simple para mantener el equilibrio. En el peor de los casos, la inserción puede requerir dos rotaciones para equilibrar el árbol. Por lo tanto, la cantidad de rotaciones en la inserción es típicamente de uno a dos en la mayoría de los casos.

Por otro lado, la eliminación en un árbol AVL puede requerir una o dos rotaciones para equilibrar el árbol en la mayoría de los casos, pero en el peor de los casos, puede requerir varias rotaciones hacia todos los centros del árbol. Esto se debe a que la eliminación puede afectar a múltiples nodos en diferentes niveles del árbol, lo que puede requerir múltiples rotaciones para restaurar el equilibrio en todo el árbol.

> [!info]
> De todas maneras, la cantidad de rotaciones máxima que se tendrían que hacer en la eliminacion es  **O(log n)**, por lo cual no empeora el peor caso.
> Lecturas recomendadas: 
> 1) [How many rotations after AVL insertion and deletion](https://cs.stackexchange.com/questions/97975/how-many-rotations-after-avl-insertion-and-deletion) 
> 2) [AVL Trees](https://courses.csail.mit.edu/6.006/spring11/rec/rec04.pdf)

# Ordenes 

Si partimos del supuesto de que el árbol AVL siempre está equilibrado, entonces tanto la inserción como la eliminación de un nodo tendrán una complejidad temporal de O(log n), donde "n" es el número de nodos en el árbol.

La inserción en un árbol AVL siempre mantiene el equilibrio, ya que después de insertar un nuevo nodo, se realiza un recorrido desde la raíz hasta el nodo insertado para actualizar los factores de balance y realizar las rotaciones necesarias para mantener el equilibrio. En cada paso, se realiza un número de operaciones proporcional a la altura del árbol, que en un árbol AVL equilibrado es **O(log n)**.

La eliminación en un árbol AVL también mantiene el equilibrio, ya que después de eliminar un nodo, se realiza un recorrido desde la raíz hasta el nodo más profundo afectado por la eliminación para actualizar los factores de balance y realizar las rotaciones necesarias para mantener el equilibrio. De nuevo, en cada paso, se realiza un número de operaciones proporcional a la altura del árbol, que en un árbol AVL equilibrado es **O(log n)**.

# AVL vs ABB

| Característica | AVL | [[ABB]] |
| --- | --- | --- |
| Balanceo | Sí, siempre equilibrado | No necesariamente equilibrado |
| Altura máxima | O(log n) | O(n) |
| Inserción | O(log n) | O(log n) en promedio, O(n) en el peor de los casos |
| Eliminación | O(log n) | O(log n) en promedio, O(n) en el peor de los casos |
| Búsqueda | O(log n) | O(log n) en promedio, O(n) en el peor de los casos |

Se recomienda usar un árbol AVL en situaciones donde la eficiencia en la inserción y eliminación de nodos es crítica. Un árbol AVL es especialmente útil en aplicaciones donde el árbol está siendo constantemente modificado y actualizado, y se requiere un equilibrio óptimo para mantener un rendimiento consistente. Por ejemplo, en aplicaciones de bases de datos, los árboles AVL se utilizan a menudo para mantener la eficiencia en la búsqueda de datos y para mantener un alto rendimiento en aplicaciones que involucran grandes cantidades de datos.

Por otro lado, un árbol binario de búsqueda (ABB) es adecuado para aplicaciones donde el equilibrio del árbol no es una prioridad. **El ABB es una estructura de datos más simple y fácil de implementar que un árbol AVL** (véase: [[Complejidad cognitiva]]), y puede ser adecuado para aplicaciones más pequeñas donde el rendimiento no es crítico. Por ejemplo, un ABB podría ser utilizado en aplicaciones de búsqueda de texto en documentos individuales, donde el número de documentos es relativamente pequeño y no se requiere una actualización constante de la estructura de datos.

> [!quote]
> "Yes, AVL-trees - this was a mistake of my youth" - ([Adelson-Velski, 2002, Radio Liberty](https://www.chessprogramming.org/Template:Quote_Donskoy_on_AVL))

# Visualización

https://www.cs.usfca.edu/~galles/visualization/AVLtree.html

# Mas info

- https://www.geeksforgeeks.org/insertion-in-an-avl-tree/