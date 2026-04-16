# Ejemplo: Programación lineal básica en Python con PuLP

En este ejemplo se muestra cómo resolver un problema de programación lineal en Python utilizando la librería PuLP.

## Modelo matemático

Maximizar:

Z = 10X + 8Y

Sujeto a:

30X + 20Y ≤ 120  
2X + 2Y ≤ 9  
4X + 6Y ≤ 24  

X, Y ≥ 0


## Paso 1: Instalar la librería PuLP

Abre la terminal y ejecuta:

```bash
pip install pulp
```

## Paso 2: Crear el archivo de código
Crea un archivo con el nombre:
```bash
python_pulp_basico.py
```

## Paso 3: Definir el problema
Se crea un modelo de maximización con la librería PuLP.
```python
from pulp import LpProblem, LpVariable, LpMaximize, LpStatus, value

modelo = LpProblem("Programacion_Lineal_Basica", LpMaximize)
```

## Paso 4: Definir las variables de decisión
Se definen las variables X y Y, indicando que no pueden tomar valores negativos.
```python
x = LpVariable("X", lowBound=0)
y = LpVariable("Y", lowBound=0)
```

## Paso 5: Definir la función objetivo
```python
modelo += 10 * x + 8 * y, "Funcion_Objetivo"
```

## Paso 6: Agregar restricciones
Se agregan las restricciones del modelo.
```python
modelo += 30 * x + 20 * y <= 120, "Restriccion_1"
modelo += 2 * x + 2 * y <= 9, "Restriccion_2"
modelo += 4 * x + 6 * y <= 24, "Restriccion_3"
```

## Paso 7: Resolver el modelo
```python
modelo.solve()
```

## Paso 8: Mostrar resultados
```python
print("Estado:", LpStatus[modelo.status])
print("Valor óptimo de Z =", value(modelo.objective))
print("X =", x.varValue)
print("Y =", y.varValue)
```

> [!NOTE]
> PuLP permite modelar problemas de programación lineal de forma clara y sencilla, por lo que es una buena opción para comenzar a trabajar optimización en Python.

> [!IMPORTANT]
> Antes de ejecutar el modelo, verifica que la función objetivo y las restricciones hayan sido escritas correctamente.

> [!WARNING]
> Un error en los signos de desigualdad o en los coeficientes puede cambiar completamente la solución del problema.
