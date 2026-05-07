# Ejemplo: Método de Jacobi en Python

## Modelo

Se busca resolver un sistema de ecuaciones lineales mediante el método iterativo de Jacobi.

El método de Jacobi consiste en:

- Representar el sistema en forma matricial  
- Despejar cada variable  
- Proponer valores iniciales  
- Actualizar las variables en cada iteración  
- Analizar si los valores convergen hacia una solución aproximada  

## Datos del problema

Se desea resolver el siguiente sistema de ecuaciones:

8x + y + z = 18  
2x + 9y + z = 24  
x + 2y + 10z = 27  

En forma matricial:

A x = b

Donde:

| Elemento | Representación |
|---|---|
| Matriz A | [[8, 1, 1], [2, 9, 1], [1, 2, 10]] |
| Vector b | [18, 24, 27] |
| Variables | x, y, z |

## Paso 1: Instalar biblioteca

```bash
pip install numpy
```

## Paso 2: Importar librería

```python
import numpy as np
```

## Paso 3: Definir matriz y vector

```python
A = np.array([
    [8, 1, 1],
    [2, 9, 1],
    [1, 2, 10]
], dtype=float)

b = np.array([18, 24, 27], dtype=float)
```

## Paso 4: Definir valores iniciales

```python
x = np.zeros(len(b))
```

## Paso 5: Definir parámetros del método

```python
max_iteraciones = 25
tolerancia = 0.0001
```

## Paso 6: Implementar método de Jacobi

```python
for iteracion in range(1, max_iteraciones + 1):

    x_nuevo = np.zeros_like(x)

    for i in range(len(A)):

        suma = 0

        for j in range(len(A)):

            if i != j:

                suma += A[i][j] * x[j]

        x_nuevo[i] = (b[i] - suma) / A[i][i]

    error = np.linalg.norm(x_nuevo - x, ord=np.inf)

    print(
        "Iteración:",
        iteracion,
        "Valores:",
        x_nuevo,
        "Error:",
        error
    )

    if error < tolerancia:

        print("El método converge.")
        break

    x = x_nuevo
```

## Paso 7: Mostrar solución aproximada

```python
print("\nSolución aproximada:")
print("x =", x_nuevo[0])
print("y =", x_nuevo[1])
print("z =", x_nuevo[2])
```

## Interpretación

La solución aproximada representa los valores de las variables que satisfacen el sistema de ecuaciones lineales de forma iterativa.

Este tipo de método se utiliza cuando:

- El sistema es grande  
- Se requiere una aproximación eficiente  
- No es conveniente resolver directamente por métodos exactos  
- Se desea analizar la convergencia del proceso  

## Código completo

```python
import numpy as np

A = np.array([
    [8, 1, 1],
    [2, 9, 1],
    [1, 2, 10]
], dtype=float)

b = np.array([18, 24, 27], dtype=float)

x = np.zeros(len(b))

max_iteraciones = 25
tolerancia = 0.0001

for iteracion in range(1, max_iteraciones + 1):

    x_nuevo = np.zeros_like(x)

    for i in range(len(A)):

        suma = 0

        for j in range(len(A)):

            if i != j:

                suma += A[i][j] * x[j]

        x_nuevo[i] = (b[i] - suma) / A[i][i]

    error = np.linalg.norm(x_nuevo - x, ord=np.inf)

    print(
        "Iteración:",
        iteracion,
        "Valores:",
        x_nuevo,
        "Error:",
        error
    )

    if error < tolerancia:

        print("El método converge.")
        break

    x = x_nuevo

print("\nSolución aproximada:")
print("x =", x_nuevo[0])
print("y =", x_nuevo[1])
print("z =", x_nuevo[2])
```

> [!NOTE]
> El método de Jacobi es un método iterativo utilizado para aproximar soluciones de sistemas de ecuaciones lineales.

> [!IMPORTANT]
> Para favorecer la convergencia, es recomendable que la matriz sea diagonalmente dominante.

> [!WARNING]
> Si el sistema no cumple condiciones adecuadas de convergencia, el método puede no estabilizarse o producir resultados incorrectos.
