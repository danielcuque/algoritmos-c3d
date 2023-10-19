# Algoritmo para manejar funciones

#### Orden del segmento reservado para funciones
1. Parámetros
2. Variables locales
3. Valor de retorno
4. Variables temporales

### Función en alto nivel
```
proc a() {
    int b;
    int c;
    b = 5;
    c = 2;
    int d;
    d=b+c;
}
```

### Función en bajo nivel
```c
// P hace referencia a la dirección reservada para el segmento de memoria de la función 'a' dentro del stack

void a() {
    t1 = P + 0;
    stack[t1] = 5;
    t2 = P + 1;
    stack[t2] = 2;
    t3 = P + 2;     // Indice
    t4 = P + 0;     
    t5 = stack[t4]  // valor b
    t6 = P+1
    t7 = stack[t6] // valor c
    t8 = t5 + t7    // valor b+c
    stack[t3] = t8
}
```

```
proc abc(int x, int y, int z){
    int b;
    int c:
    b = 5; 
    c = 2;
    int d;
    d = b+c*x/z-y;
}
```

0 - int y - parámetro 1
1 - int y - parámetro 2
2 - int z - parámetro 3
3 - int b - variable local 1
4 - int c - variable local 2
5 - int d - variable local 3


```c
void ab() {
    t9 = p + 3;     
    stack[t9] = 5;
    t10 = p+4
    stack[t10] = 2;
    t11 = p + 3;
    t12 = stack[t11];   // valor b
    t13 = p + 4;
    t14 = stack[t13];   // valor c
    t15 = p + 0 
    t16 = stack[t15]    // valor x
    t17 = t14 + t16     // valor c + x
    t18 = p + 2;
    t19 = stack[t18]    // valor z
    t20 = t17 / t19     // valor c * x / z
    t21 = t12 + t20    // valor b + c * x / z
    t22 = p + 1
    t23 = stack[t22]    // valor y
    t24 = t21 - t23     // valor b + c * x / z - y
}
```

0 - int x - parámetro 1
1 - int y - parámetro 2
2 - int z - parámetro 3
3 - int w - variable local 1
4 - int - valor de retorno

Tamaño del procedimiento = 5

```
function int a(int x, int y, int z){
    int w;
    w = x + y + z;
    w = w * 100;
    return w;
}
```

```c
void a(){
    t1 = p + 3;    // indice w
    t2 = p + 0     // indice x
    t3 = stack[t2] // valor x
    t4 = p + 1     // indice y
    t5 = stack[t4] // valor y
    t6 = t3 + t5   // valor x + y
    t7 = p + 2     // indice z
    t8 = stack[t7] // valor z
    t9 = t6 + t8   // valor x + y + z
    stack[t1] = t9 // w = x + y + z
    t10 = p + 3    // indice w
    t11 = p + 3    // indice w
    t12 = stack[t11] // valor w
    t13 = t12 * 100  // valor w * 100
    stack[t10] = t13 // w = w * 100
    t14 = p + 4     // indice de retorno
    t15 = p + 3     // indice w
    t16 = stack[t15] // valor w
    stack[t14] = t16 // retorno = w
    goto L1
    L1:
}
```

0 - int t - parámetro 1
1 - int q - parámetro 2
2 - int r - parámetro 3
3 - int s - variable local 1

Tamaño del procedimiento = 4

```
function b(int t, int q, int r){
    int s;
    s = a(t, q, r);
    s = s * 200;
}
```

```c
void b() {
    t17 = p + 3     // Indice s
    t18 = p + 4     // p + tamaño de la función en el stack
    t19 = t18 + 0
    t20 = p + 0;        // Indice t
    t21 = stack[t20]    // Valor t
    stack[t19] = t21    
    t22 = t18 + 1  
    t23 = p + 1
    t23 = stack[t23]    // val q
    stack[t22] = t23    // parametro 1 de a()
    t25 = t18 + 2  
    t26 = p + 2
    t27 = stack[t26]    // valor r
    stack[t25] = t27    // parametro 2 de a() 
    a();
    t28 = p + 4
    t29 = stack[t28]
    p = p - 4
    stack[t17] = t29
    t30 = p+3
    t31 = p + 3
    t32 = stack[t31]
    t33 = t32 * 200
    stack[t31] = t33
}
```


0 - int num1 - parámetro 1
1 - int num2 - parámetro 2
2 - int num3 - variable local 1
3 - int valor de retorno

```
function int suma(int num1, int num2){
    int num3 = num1+num2;
    return num3;
}
```

```c
void suma(){
    t1 = p + 2      // Indice num3
    t2 = p + 0;     // Indice num1
    t3 = stack[t2]  // Valor num1
    t4 = p + 1;     // Indice num2
    t5 = stack[t4]  // Valor num2
    t6 = t3 + t5    // Valor num1 + num2
    stack[t1] = t6  // num3 = num1 + num2

    t7 = p + 3      // Indice de retorno
    t8 = p + 2      // Indice num3
    t9 = stack[t8]  // Valor num3
    stack[t7] = t9  // retorno = num3

    goto L1;

    L1:
}
```

0 - int num1 - parámetro 1
1 - int num2 - parámetro 2
2 - int num3 - variable local 1
3 - int valor de retorno


```
function int multiplicacion(int num1, int num2){
    int num3 = num1*num2;
    return num3;
}
```

```c
void multiplicacion(){
    t10 = p + 2     // Indice num3
    t11 = p + 0;    // Indice num1
    t12 = stack[t11] // Valor num1
    t13 = p + 1;    // Indice num2
    t14 = stack[t13] // Valor num2
    t15 = t12 * t14 // Valor num1 * num2
    stack[t10] = t15 // num3 = num1 * num2

    t16 = p + 3     // Indice de retorno
    t17 = p + 2     // Indice num3
    t18 = stack[t17] // Valor num3
    stack[t16] = t18 // retorno = num3

    goto L1;

    L1:
}
```

0 - int s - variable local 1

```
function operaciones() {
    int s;
    s = multiplicacion(5, 10) - suma(5, 10);
}
```

```c

void operaciones() {
    t19 = p + 0    // Indice s

    t20 = p + 1    // p + tamaño de la función en el stack

    t21 = t20 + 0 
    stack[t21] = 5 // Parametro 1
    
    t22 = t20 + 1
    stack[t22] = 10 // Parametro 2
    p = p + 1
    multiplicacion();
    t23 = p + 3
    t24 = stack[t23]    // Valor de retorno de multiplicacion

    p = p - 1

    t25 = p + 1

    t26 = t25 + 0
    stack[t26] = 5 // Parametro 1

    t27 = t25 + 1
    stack[t27] = 10 // Parametro 2

    p = p + 1
    suma();
    t28 = p + 3

    t29 = stack[t28]    // Valor de retorno de suma

    p = p - 1

    t30 = t24 - t29     // Valor de retorno de multiplicacion - Valor de retorno de suma

    stack[t19] = t30    // s = multiplicacion(5, 10) - suma(5, 10)

}

```

# Recursivas

Las variables temporales pueden ser globales y las podemos sobreescribir

0 - int num - parámetro 1
1 - int     - retorno



```
function int factorial(int num){
    if(num <= 0){
        return 1;
    } else {
        return num * factorial(num-1);
    }
}
```

```c
void factorial() {
    t1 = p + 0     // Indice num
    t2 = stack[t1]  // Valor num

    if t2 <= 0 goto L1
    goto L2
    L1:
    t3 = p + 1
    stack[t3] = 1
    
    
    goto L3
    goto L4
    
    L2:
    t4 = p + 1      // Indice de retorno
    t5 = p + 0      // Indice num
    t6 = stack[t5]  // Valor num
    t7 = p + 2      // p + tamaño de la función en el stack
    t8 = t7 + 0
    t9 = p + 0      // Indice num
    t10 = stack[t9] // Valor num
    t11 = t10 - 1   // Valor num - 1
    stack[t8] = t11 // Parametro 1
    p = p * 2;
    factorial();
    t12 = p + 1;
    t13 = stack[t12] // Valor de retorno de factorial
    p = p - 2
    t14 = t6 * t13   // Valor num * factorial(num-1)

    stack[t4] = t14  // retorno = num * factorial(num-1)
    goto L5;
    L4:
    L3:
    L5:

}

```