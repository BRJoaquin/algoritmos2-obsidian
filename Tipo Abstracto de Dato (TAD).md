# Intro
Un tipo abstracto de datos (TAD) es una abstracción matemática que describe una colección de objetos y las operaciones que se pueden realizar sobre ellos. Un TAD define una interfaz pública que especifica **qué operaciones están disponibles y cómo se pueden utilizar**, pero oculta los detalles internos de la implementación. 

Esto significa que los usuarios de un TAD pueden utilizarlo sin conocer los detalles de cómo está implementado, lo que les permite concentrarse en su funcionalidad y en la forma en que se utilizan sus operaciones.

Un ejemplo común de un TAD es una [[Lista]]. Una lista es una colección de elementos ordenados que se pueden agregar, eliminar, buscar y modificar. Sin embargo, la forma en que se implementa una lista puede variar considerablemente dependiendo del lenguaje de programación y de los requisitos específicos de la aplicación. Al proporcionar una interfaz abstracta para la lista, un TAD permite que los usuarios utilicen la lista sin preocuparse por cómo está implementada.

# Ejemplos de TADs

A continuación se presentan algunos ejemplos comunes de tipos abstractos de datos:

1. [[Lista]]: Una colección de elementos ordenados que se pueden agregar, eliminar, buscar y modificar.
   
2. [[Cola]]: Una colección de elementos donde el primero que entra es el primero en salir (FIFO). Las operaciones comunes incluyen agregar elementos a la cola y retirar elementos de la cabeza.
   
3. [[Pila]]: Una colección de elementos donde el último en entrar es el primero en salir (LIFO). Las operaciones comunes incluyen agregar elementos a la pila y retirar elementos de la cima.
 
4. Árbol: Una colección de elementos organizados jerárquicamente, donde cada elemento tiene un padre y cero o más hijos. Las operaciones comunes incluyen insertar elementos en el árbol y buscar elementos.
   
5. [[Grafo]]: Una colección de nodos y aristas que se utilizan para representar relaciones entre elementos. Las operaciones comunes incluyen agregar nodos y aristas al grafo y buscar caminos entre nodos.
   
6. [[Set]]: Una colección de elementos únicos que se pueden agregar, eliminar y verificar si un elemento está en el conjunto.
   
7. [[Tabla]]: Una colección de pares clave-valor donde cada clave se utiliza para recuperar su valor correspondiente. Las operaciones comunes incluyen agregar pares clave-valor al mapa y buscar valores por clave.

# TAD vs Estructura de datos

La principal diferencia entre los tipos abstractos de datos (TAD) y las [estructuras de datos](Estructura%20de%20datos.md de datos/! Estructura de datos>) es que los TAD **se centran en la funcionalidad** y la interfaz pública de una colección de datos, mientras que las estructuras de datos **se centran en la forma en que los datos se organizan y almacenan en la memoria**.

Un TAD define una abstracción matemática que describe una colección de objetos y las operaciones que se pueden realizar sobre ellos, y oculta los detalles de cómo se implementa la colección. Por otro lado, una estructuras de datos describe cómo se organizan los datos en la memoria y cómo se accede a ellos de manera eficiente.

Sin embargo, los TAD y las estructuras de datos están estrechamente relacionados. De hecho, **muchas estructuras de datos se utilizan para implementar TAD**. Por ejemplo, una [[Lista simplemente encadenada]] se puede utilizar para implementar una [[Lista]] abstracta de datos, y una [[Tabla de hash]] se puede utilizar para implementar una [[Tabla]] (abstracta de datos). En este sentido, una estructura de datos es la implementación concreta de un TAD.

En resumen, los TAD se enfocan en la funcionalidad y la interfaz pública de una colección de datos, mientras que las estructuras de datos se enfocan en cómo se organizan los datos en la memoria. A menudo, las estructuras de datos se utilizan para implementar TAD.

# Importancia de los TADs

Los tipos abstractos de datos (TAD) son importantes por varias razones:

1.  **Abstracción**: Los TAD proporcionan una abstracción de alto nivel que permite a los programadores concentrarse en la funcionalidad y la interfaz pública de una colección de datos, en lugar de preocuparse por los detalles de cómo se implementa.

3.  **Modularidad**: Los TAD permiten a los programadores modularizar su código y separar las preocupaciones, lo que puede hacer que el código sea más fácil de entender, mantener y depurar.

3.  **Reutilización de código**: Los TAD pueden ser utilizados por diferentes programas y por diferentes desarrolladores, lo que puede aumentar la reutilización de código y ahorrar tiempo y esfuerzo en el desarrollo de software.

4.  **Eficiencia**: Los TAD pueden ser implementados de varias maneras, lo que permite a los programadores elegir la implementación más eficiente para un problema específico.

5.  **Flexibilidad**: Los TAD pueden ser combinados y utilizados en conjunto para resolver problemas más complejos.

En resumen, los TAD son importantes porque proporcionan **una abstracción de alto nivel** que facilita la programación modular, la reutilización de código y la selección de implementaciones eficientes.

# Mas informacion

- https://www.geeksforgeeks.org/abstract-data-type
- https://en.wikipedia.org/wiki/Abstract_data_type