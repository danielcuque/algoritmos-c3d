# Manejo de vectores y matrices en C3D

Algoritmo para el manejo de vectores y matrices en C3D.

### Vectores:

A[i]

Fórmula:

(i - i1)

### Matriz de 3 dimensiones:

A[i][j][k] 

La fórmula para obtener la posición es la siguiente:

((i-i1) * n2 + j - i2) * n3 + k - i3

Donde:

### Matriz de 4 dimensiones:

A[i][j][k][l]

Fórmula:

(((i-i1) * n2 + j - i2) * n3 + k - i3) * n4 + l - i4

### Matriz de n dimensiones:

A[i1][i2][i3]...[in]

Fórmula:

((((((i1-i1) * n2 + i2 - i2) * n3 + i3 - i3) * n4 + i4 - i4) * n5 + i5 - i5) * n6 + i6 - i6) * ... * n(n) + in - in

Lo único que cambia es la primera posición, el resto es igual.

### Ejemplo:

```swift

var A = Array(repeating: Array(repeating: Array(repeating: 0, count: 13), count: 5), count: 13)

for i in 7...12 {
    for j in 4...8 {
        for k in 12...24 {
            A[i - 7][j - 4][k - 12] = i + j + k
        }
    }
}

array[8][6][array[9][7][array[10][8][15]]] = array[8][7][14]
```

Se quiere modificar el arreglo *array* en la posición

i = 8

j = 6

k = array[9][7][array[10][8][15]]

Por lo tanto debemos de cuatro veces al arreglo *array*.

El cuarto arreglo que se obtiene es: array[10][8][15]

El tercer arreglo que se obtiene es: array[9][7][array[10][8][15]]

El segundo arreglo que se obtiene es: array[8][7][14]

El primer arreglo que se obtiene es: array[8][6][array[9][7][array[10][8][15]]]

Donde:

i1 = 7  | i2 = 4 | i3 = 12
s1 = 12 | s2 = 8 | s3 = 24
n1 = 6  | n2 = 5 | n3 = 13

Para calcular *n* se usa la siguiente fórmula:

s1 - i1 + 1

### C3D:

((i-i1) * n2 + j - i2) * n3 + k - i3

```c

// Accesso al primer arreglo de 3 dimensiones

t1 = 8 - 7      // i - i1
t2 = t1 * 5     // (i - i1) * n2
t3 = t2 + 6     // (i - i1) * n2 + j
t4 = t3 - 4     // (i - i1) * n2 + j - i2

// Debemos de calcular el valor de n3 antes de continuar

t5 = 9 - 7     // s1 - i1
t6 = t5 * 5    // (s1 - i1) * n2
t7 = t6 + 7    // (s1 - i1) * n2 + j
t8 = t7 - 4    // (s1 - i1) * n2 + j - i2

// Debemos de calcular el valor de n3 antes de continuar

t9 =  10 - 7    // s1 - i1
t10 = t9 * 5    // (s1 - i1) * n2
t11 = t10 + 8   // (s1 - i1) * n2 + j
t12 = t11 - 4   // (s1 - i1) * n2 + j - i2
t13 = t12 * 13  // ((s1 - i1) * n2 + j - i2) * n3
t14 = t13 + 15  // ((s1 - i1) * n2 + j - i2) * n3 + k
t15 = t14 - 12  // ((s1 - i1) * n2 + j - i2) * n3 + k - i3
t16 = array[t15] // array[((s1 - i1) * n2 + j - i2) * n3 + k - i3]

// Accesso al segundo arreglo de 3 dimensiones
t17 = t8 * 13   // ((i - i1) * n2 + j - i2) * n3
t18 = t17 + t16 // ((i - i1) * n2 + j - i2) * n3 + array[((s1 - i1) * n2 + j - i2) * n3 + k - i3]

t19 = t18 - 12  // ((i - i1) * n2 + j - i2) * n3 + array[((s1 - i1) * n2 + j - i2) * n3 + k - i3] - i3

t20 = A[t19]
t21 = t4 * 13  // ((i - i1) * n2 + j - i2) * n3
t22 = t21 + t20 // ((i - i1) * n2 + j - i2) * n3 + A[((i - i1) * n2 + j - i2) * n3 + array[((s1 - i1) * n2 + j - i2) * n3 + k - i3] - i3]
t23 = t22 - 12 // ((i - i1) * n2 + j - i2) * n3 + A[((i - i1) * n2 + j - i2) * n3 + array[((s1 - i1) * n2 + j - i2) * n3 + k - i3] - i3] - i3

// Calcular indice en el que se asigna el valor

t24 = 8 - 7
t25 = t24 * 5
t26 = t25 + 7
t27 = t26 - 4
t28 = t27 * 13
t29 = t28 + 14
t30 = t29 - 12
t31 = array[t30]
A[t23] = t31
```