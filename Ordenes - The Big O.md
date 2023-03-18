# Orden temporal

El orden temporal de un algoritmo se refiere a la cantidad de tiempo que tarda un algoritmo en completar su tarea, medida en función del tamaño de la entrada. Los ordenes temporales más comunes se expresan en notación asintótica, como la notación Big O.

La notación Big O describe el comportamiento asintótico del tiempo de ejecución del algoritmo en el peor de los casos. Algunos de los órdenes temporales más comunes son:

- O(1): Tiempo constante. El tiempo de ejecución del algoritmo no depende del tamaño de la entrada. Un ejemplo de algoritmo con orden O(1) es el siguiente:
```cpp
int sum(int a, int b) {
    return a + b;
}
```

- O(log n): Tiempo logarítmico. El tiempo de ejecución del algoritmo crece de manera proporcional al logaritmo del tamaño de la entrada. Un ejemplo de algoritmo con orden O(log n) es la búsqueda binaria:

```cpp
int binarySearch(int arr[], int l, int r, int x) {
    while (l <= r) {
        int m = l + (r-l)/2;
        if (arr[m] == x)
            return m;
        if (arr[m] < x)
            l = m+1;
        else
            r = m-1;
    }
    return -1;
}
```

- O(n): Tiempo lineal. El tiempo de ejecución del algoritmo crece de manera proporcional al tamaño de la entrada. Un ejemplo de algoritmo con orden O(n) es la suma de los elementos de un arreglo: 
  
```cpp
int sumArray(int arr[], int n) {
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }
    return sum;
}
```

- O(n log n): Tiempo log-lineal. El tiempo de ejecución del algoritmo crece de manera proporcional al tamaño de la entrada multiplicado por su logaritmo. Un ejemplo de algoritmo con orden O(n log n) es el algoritmo de ordenamiento QuickSort:
  
```cpp
void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}
```

- O(n^2): Tiempo cuadrático. El tiempo de ejecución del algoritmo crece de manera proporcional al cuadrado del tamaño de la entrada. Un ejemplo de algoritmo con orden O(n^2) es el algoritmo de ordenamiento por selección:
  
```cpp
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        int min_idx = i;
        for (int j = i+1; j < n; j++)
            if (arr[j] < arr[min_idx])
                min_idx = j;
        swap(arr[min_idx], arr[i]);
    }
}
```

- O(2^n): Tiempo exponencial. El tiempo de ejecución del algoritmo crece de manera exponencial con el tamaño de la entrada. Un ejemplo de algoritmo con orden O(2^n) es el problema de la mochila, que busca encontrar la combinación óptima de elementos para llenar una mochila con una capacidad dada. El algoritmo de fuerza bruta para este problema tiene un orden temporal de O(2^n), ya que debe generar todas las posibles combinaciones de elementos para encontrar la solución óptima.
  
```cpp
#include <iostream>
using namespace std;

int max(int a, int b) {
    return (a > b) ? a : b;
}

int knapsack(int W, int wt[], int val[], int n) {
    if (n == 0 || W == 0)
        return 0;
    if (wt[n-1] > W)
        return knapsack(W, wt, val, n-1);
    else
        return max(val[n-1] + knapsack(W-wt[n-1], wt, val, n-1), knapsack(W, wt, val, n-1));
}

int main() {
    int val[] = {60, 100, 120};
    int wt[] = {10, 20, 30};
    int W = 50;
    int n = sizeof(val)/sizeof(val[0]);
    cout << "Valor máximo posible: " << knapsack(W, wt, val, n) << endl;
    return 0;
}
```

![[bigo.png]]

Es importante tener en cuenta el orden temporal de un algoritmo al seleccionar la mejor solución para un problema determinado, ya que un algoritmo más eficiente puede hacer una gran diferencia en el tiempo de ejecución y el rendimiento general del programa.

## Casos 

En el análisis de algoritmos, se pueden considerar diferentes casos para evaluar el rendimiento de un algoritmo en función de diferentes entradas. Los casos comúnmente considerados son el mejor caso, el peor caso y el caso promedio.

El **mejor caso** se refiere al escenario en el que el algoritmo tiene el menor tiempo de ejecución posible para una entrada dada. Es decir, es el caso en el que el algoritmo se desempeña mejor. Por ejemplo, el mejor caso para una búsqueda binaria en un arreglo ordenado es cuando el elemento buscado está en el medio del arreglo.

El **peor caso** se refiere al escenario en el que el algoritmo tiene el mayor tiempo de ejecución posible para una entrada dada. Es decir, es el caso en el que el algoritmo se desempeña peor. Por ejemplo, el peor caso para una búsqueda lineal en un arreglo es cuando el elemento buscado no se encuentra en el arreglo y se debe recorrer todo el arreglo.

El **caso promedio** se refiere al rendimiento esperado del algoritmo para entradas aleatorias. Se calcula como el promedio del tiempo de ejecución del algoritmo para todas las posibles entradas. Este caso es importante para evaluar el rendimiento del algoritmo en situaciones reales en las que no se conoce de antemano el tipo de entrada que se va a procesar.

Es importante tener en cuenta que el mejor caso, el peor caso y el caso promedio pueden ser muy diferentes entre sí, y cada uno proporciona información valiosa sobre el rendimiento del algoritmo en diferentes escenarios. Por lo tanto, es importante considerarlos todos al analizar y comparar diferentes algoritmos.

# Orden espacial

El orden espacial de un algoritmo se refiere a la cantidad de memoria adicional que se requiere para ejecutar el algoritmo, medida en función del tamaño de la entrada. En otras palabras, el orden espacial describe la cantidad de espacio de memoria que utiliza un algoritmo para realizar su tarea.

El orden espacial de un algoritmo puede ser muy importante en situaciones en las que la memoria es limitada o costosa, como en sistemas embebidos o en dispositivos móviles. Algunos algoritmos tienen un orden espacial constante, es decir, utilizan una cantidad fija de memoria, independientemente del tamaño de la entrada. Otros algoritmos tienen un orden espacial variable, que depende del tamaño de la entrada.

Es importante tener en cuenta tanto el orden temporal como el orden espacial de un algoritmo al seleccionar la mejor solución para un problema determinado. A menudo, hay un compromiso entre la eficiencia temporal y espacial de un algoritmo, y es importante encontrar el equilibrio adecuado entre ambos para lograr el mejor rendimiento general.

# Mas información

- https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/
- https://www.freecodecamp.org/news/big-o-cheat-sheet-time-complexity-chart/

<iframe width="560" height="315" src="https://www.youtube.com/embed/RATueyCIN80" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
