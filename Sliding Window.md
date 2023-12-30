# Sliding Window
* Se usa cuando querés operar en un subset de tamaño específico (ventana) de un array o lista.
* La ventana se va desplazando desde el inicio hasta el fin del array.
* Observar un elemento a la vez.

### Cómo identificar
* El tipo de dato con el que se trabaja es *lista*, *array* o *string*.
* Encontrar un substring de cierta característica.
* Analizar una porción de una estructura lineal, que tenga un tamaño determinado (aunque sea con una letra).

### Ejemplos:
* Max subarray sum de tamaño *k*.
* El substring más largo con *k* caracteres distintos.
* Anagramas en string.

### Pseudocódigo

Dado un array de enteros "arr" y 2 enteros: k y threshold, devolver el número de sub-arrays tamaño k y promedio mayor o igual al threshold.

1. Encontrar la suma de los primeros *k* ints
2. Agregar al contador si el promedio de ellos cumple con la consigna.
3. Para el resto del array:
  <ol type="a">
    <li>"Deslizar" la ventana de a un elemento.</li>
    <li>Calcular el promedio de esos k elementos.</li>
    <li>Si el promedio de esos k elementos es mayor al threshold, incrementar el contador.      </li>
  </ol> 

4. Devolver contador.

```
int sumOfSubArrays (List<int> arr, int k, int threshold)
{
  //operar con los k primeros  
  int sum = 0;
  for (int i = 0; i < k; i++)
  {
    sum+=arr[i];
  }
  // agregar al contador si el promedio de ellos cumple la consigna
  int counter = 0;
  if (sum/k >= threshold) counter++;

  // j apunta al ultimo de la ventana, por eso empieza en k
  // imaginemos que la ventana se desplaza un lugar, hacia la derecha por vuelta
  for (int j = k; j < arr.Count; j++)
  {
    // para no sumar al pedo, utilizo el sum que ya tenía, por eso no lo pongo a cero.

    // solo que saco el valor que ya no está en la ventana.
    sum-= arr.ElementAt(j-k);
    // y sumo el que ahora es el último
    sum+= arr.ElementAt(j);
    if (sum/k >= threshold) counter++;
  }
  return counter;
}
```
