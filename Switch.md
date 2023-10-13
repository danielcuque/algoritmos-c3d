# Algoritmo para el switch en C3D

## Codigo en Swift

```swift
let numero = 2
switch numero {
case 1:
print("Uno")
case 2:
print("Dos")
case 3:
print("Tres")
default:
print("Invalid day")
}

```

## Codigo en C3D

```c
t1 = 2
stack[P] = t1

t2 = stack[P]

salida = L1
case1 = L2
case2 = L3
case3 = L4
default = L5

-- Case 1
L2:
if(t2 != 1) goto L3
[block]
goto L1

L3:
if(t2 != 2) goto L4
[block]
goto L1

L4:
if(t2 != 3) goto salida/default // Verificar si existe el default

[block]
goto L1

L5:
[block]
goto L1

L1:
```


